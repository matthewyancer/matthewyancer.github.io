## Building Jarvis in C#, Part 6: Speech-to-Text

This post is a continuation [of](https://www.matthewyancer.com/2024/01/16/building-jarvis-in-csharp-part-1.html) [the](https://www.matthewyancer.com/2024/01/23/building-jarvis-in-csharp-part-2.html) [Building](https://www.matthewyancer.com/2024/01/30/building-jarvis-in-csharp-part-3.html) [Jarvis](https://www.matthewyancer.com/2024/02/08/building-jarvis-in-csharp-part-4.html) [series](https://www.matthewyancer.com/2024/02/10/building-jarvis-in-csharp-part-5.html).

In the last couple posts, we have been gearing up for the integration of speech-to-text capabilities into our Jarvis AI assistant. First, we needed a way to trigger speaking to Jarvis. For this, we built a [push-to-talk](https://www.matthewyancer.com/2024/02/08/building-jarvis-in-csharp-part-4.html) button. Then, we needed a way to record speech into our application. So, we built [cross-platform audio](https://www.matthewyancer.com/2024/02/10/building-jarvis-in-csharp-part-5.html) capabilities for microphone and sound mixing. With these in place, we have all of the necessary prerequisites to now build speech-to-text. So, let's get to it.

### Selecting Our Speech-To-Text Library

There are a variety of speech-to-text libraries, applications, and APIs available. After having a generally good experience with eSpeak NG for local [text-to-speech](https://www.matthewyancer.com/2024/01/23/building-jarvis-in-csharp-part-2.html), I thought I would test out a locally running speech-to-text product. So, my first tests were with the [pocketsphinx](https://github.com/cmusphinx/pocketsphinx) command-line program from [CMU Sphinx](https://cmusphinx.github.io/). I used a System.Diagnostics.Process class to execute pocketsphinx, redirecting input so I could route in microphone data and redirecting output so that I could receive the text output. It worked perfectly. As I tested pocketsphinx, I found that sometimes it would capture my speech exactly. But other times, it would get it wrong, very wrong. None-of-the-same-words wrong. I found that [enunciation](https://www.youtube.com/watch?v=0ISJS4gSBh0) helped to a degree. But the accuracy rate still wasn't where I wanted it and speaking with heavy enunciation quickly becomes exhausting. I don't want to discount pocketsphinx. It's a good product. I think that it would work well for an embedded device with no internet connection running a limited vocabulary with a defined dictionary. But we need to consider other options for our use case.

While integrating the GPT LLM model for our [conversational chat](https://www.matthewyancer.com/2024/01/16/building-jarvis-in-csharp-part-1.html), I noticed that OpenAI also had a speech-to-text option available, known as [Whisper](https://openai.com/research/whisper). And there was support for it in the Azure.AI.OpenAI NuGet package that we were already using. So, I wired it up and gave it a test. Immediate night-and-day difference. Spooky levels of accuracy. No [enunciation](https://www.youtube.com/watch?v=uNe7x13q2MU) required. Talking back and forth with Jarvis became a [magical](https://www.youtube.com/watch?v=MX0D4oZwCsA) experience. Whisper is killer tech. It is exciting to see that OpenAI has open sourced it and posted it to [GitHub](https://github.com/openai/whisper).

Let's look at how to add it to our system.

### Integrating Whisper

In the full source code for the [forth post](https://www.matthewyancer.com/2024/02/08/building-jarvis-in-csharp-part-4.html) in this series, I had included a stubbed version of the SpeechToText class. We'll be filling this in, starting with member variables and the constructor:

```csharp
private readonly SoundMixer m_SoundMixer;
private readonly Microphone m_Microphone;
private readonly SpeechToTextSettings m_Settings;
private readonly string m_OpenAiKey;

private int m_SavedMixerVolume = 100;

public SpeechToText(SoundMixer soundMixer, Microphone microphone, SpeechToTextSettings settings, string? openAiKey)
{
    if(string.IsNullOrEmpty(openAiKey))
        throw new ArgumentNullException(nameof(openAiKey));

    m_SoundMixer = soundMixer ?? throw new ArgumentNullException(nameof(soundMixer));
    m_Microphone = microphone ?? throw new ArgumentNullException(nameof(microphone));
    m_Settings = settings ?? throw new ArgumentNullException(nameof(settings));

    m_OpenAiKey = openAiKey;
}
```

We use the constructor to pass in the dependencies that we will rely on while performing our speech-to-text operations. In my testing, I have found that if you use the push-to-talk feature while Jarvis is in the middle of speaking, he will record his own voice and then start talking to himself. To prevent this, we will use the SoundMixer class to adjust the master volume while the push-to-talk button is being held down so that Jarvis's voice won't be picked up by the microphone. In addition to the SoundMixer class, we will also need the Microphone class for recording our voice. And then we need to pass in speech-to-text settings and the OpenAI key for accessing the Whisper API. All of these items are set to member variables in the SpeechToText class so that we can access them later.

Next, we need to handle the PushToTalkPressing event:

```csharp
public void PushToTalkPressing(object? sender, EventArgs e)
{
    Task.Run(async () =>
    {
        m_SavedMixerVolume = await m_SoundMixer.GetVolumeAsync();

        int reducedVolumeLevel = Convert.ToInt32(m_Settings.ReducedVolumeLevel);

        if (m_SavedMixerVolume > reducedVolumeLevel)
            m_SoundMixer.SetVolume(reducedVolumeLevel);  //reduce volume so Jarvis doesn't talk to himself
    }).Wait();

    m_Microphone.StartRecording();
}
```

Our previous work on the SoundMixer and Microphone classes is really helping simplify things here. We first retrieve the current volume level and store it in a member variable. We retrieve the setting for the reduced volume level we should set. If the current volume is greater than the reduced volume level, we update the system volume to the new reduced level. Once the volume is adjusted, we use the microphone to start recording. Recording will continue for as long as the push-to-talk button is held down.

Now let's look at how we handle the PushToTalkPressed event:

```csharp
public string? PushToTalkPressed(object? sender, EventArgs e)
{
    string? result = null;

    byte[] microphoneData = m_Microphone.StopRecording();

    //restore volume to previous level
    m_SoundMixer.SetVolume(m_SavedMixerVolume);

    if (microphoneData.Length > 0)
    {
        //set whisper api options
        AudioTranscriptionOptions transcriptionOptions = new()
        {
            DeploymentName = "whisper-1",
            Language = m_Settings.Language,
            ResponseFormat = AudioTranscriptionFormat.Simple,
            Filename = "speechtotext.wav",
            AudioData = BinaryData.FromBytes(microphoneData)
        };

        //use whisper api to convert speech to text
        OpenAIClient openAiClient = new(m_OpenAiKey);
        Azure.Response<AudioTranscription> openAiResponse =
            openAiClient.GetAudioTranscription(transcriptionOptions);
        result = openAiResponse.Value.Text;
    }

    return result;
}
```

Once the user releases the push-to-talk button, we tell the microphone to stop recording. We then restore the system volume to the previously saved level. If we receive back microphone data, we set the Whisper API options and pass in the microphone data. Note that the filename parameter is only used for its file extension to tell Whisper the format of the audio data. We then call the Whisper API and receive the transcription response. And that's it! We've successfully converted speech into text.

Please note that in my testing, the call to Whisper and the subsequent call to the GPT model tend to happen pretty rapidly. Occasionally, one or the other can take a little while to respond. Our chat application will pause with the cursor blinking while waiting for responses.

### Strange Behavior

I've noticed some rather interesting but strange behaviors if I rapidly press and release the push-to-talk button. Without speaking and with no other sounds in the room, I will get a response from Whisper. It is often the word "You" and occasionally "Thank you." At first, I thought the microphone was picking up the sound of the key press itself and interpreting it as the word "You". But then I had this string get returned while trying to reproduce the issue: "Subs by www.zeoranger.co.uk." You can imagine my surprise. I wondered if there was a very quiet video playing somewhere else in the house. I'm not going to lie, I actually had a moment where I wondered if I had accidentally overflowed my memory access somewhere and read a string from another part of memory. LOL. And then I had this come through: "Go to Beadaholique.com for all of your beading supply needs!". And then this one: "Okay guys, have a good one another day. Thanks for watching and see you in the next one." Keep in mind that I'm just pressing the push-to-talk button super quick, less than a second, in a quiet room.

After researching this a bit, I found [this](https://www.reddit.com/r/OpenAI/comments/18yqlw6/weird_behaviour_in_whisper_model/) answer. It appears that the training for Whisper included using YouTube videos for audio and their transcripts for text. There are times at the end of these videos where dead air or no sound is being played but the transcript itself continues to have text, such as "Subs by www.zeoranger.co.uk" or a delayed "Thank you." This has trained the Whisper model to think that different non-speaking dead air sounds are these various phrases. Wild, huh? I will have to continue to look into this. I'm thinking a fix would involve not submitting very short audio clips to the Whisper API. It will require some experimentation to get the right setting and not cut off legitimate short messages. Stay tuned.

### Conclusion

Well, it took a few posts to get there, but we've done it! We have successfully added speech-to-text to our system.

With this in place, I'm realizing that another issue is going to start to rear its head soon. The longer I leave Jarvis running, and send messages back and forth with him, the more likely I am to hit his token limit. The currently configured model, gpt-3.5-turbo-0125, has a token limit of 16,385. We'll need to investigate strategies for keeping him within his token limit. In the mean time, you can restart him periodically or you can change the configuration setting for his model to one of the GPT 4 [models](https://platform.openai.com/docs/models/overview) to gain access to a 128,000 token limit to give yourself more breathing room. Just keep in mind that the API will charge you at a higher [rate](https://openai.com/pricing).

While we're on the subject of workarounds, I had posted a couple comments to the [second post](https://www.matthewyancer.com/2024/01/23/building-jarvis-in-csharp-part-2.html) in this series recently regarding an issue with eSpeak NG on Windows only. There is a bug in the 1.51 release of eSpeak NG that leads to choppiness in the audio on Windows. A fix has been submitted to the project on GitHub, but it has not been released in an updated MSI installer. As a workaround to the issue, if it bothers you, switch to the original eSpeak 1.48.04 which is available [here](https://espeak.sourceforge.net/download.html). When you install, make sure you include the voice for "en-gb" so that you will have access to Jarvis's voice. You will need to add the eSpeak folder to your PATH environment variable, as the installer doesn't do it automatically. Once installed, you can adjust two settings in Jarvis's appsettings.json config file to make use of eSpeak in place of eSpeak NG. In the "TextToSpeech" section, change "ExecutableName" from "espeak-ng" to "espeak" and change "Voice" from "en-gb-x-rp" to "en-gb". And that's it; you'll be using eSpeak in Windows without choppy audio. I hope that helps.

As always, for Jarvis’s full source code, feel free to check out my GitHub repository [here](https://github.com/matthewyancer/Projects/tree/main/src/Jarvis). All code was written in C# 10 on .NET 6 using Visual Studio Code and the C# Dev Kit extension on Linux, also tested in Visual Studio 2022 on Windows.
