## Building Jarvis in C#, Part 3: Prompting and Date/Time

Continuing [my](https://www.matthewyancer.com/2024/01/16/building-jarvis-in-csharp-part-1.html) [series](https://www.matthewyancer.com/2024/01/23/building-jarvis-in-csharp-part-2.html) on creating a Jarvis AI assistant, let's explore prompting and date/time handling.

If you ask Jarvis questions related to the current date or time, you'll quickly discover that he randomly spits out answers, none of which are remotely correct:

![Jarvis Date/Time Chat - A](/assets/images/jarvis-chat-3a.png)  
(Image: Jarvis doesn't know today's date and time.)

![SpongeBob: 5 Minutes Later](/assets/images/five-minutes-later.jpg)

![Jarvis Date/Time Chat - B](/assets/images/jarvis-chat-3b.png)  
(Image: Jarvis gives an entirely different wrong answer.)

'As an AI language model', Jarvis was frozen at the moment his model was created. We must initialize Jarvis with any rules or facts we need as part of the prompt. Before we look at how to include date and time information, let's review Jarvis's current prompt.

### Jarvis's Prompt

The initial prompt from the [first post](https://www.matthewyancer.com/2024/01/16/building-jarvis-in-csharp-part-1.html) in this series forms the personality basis for the responses we receive from the OpenAI API:

```csharp
string prompt = "Please act as an AI assistant named Jarvis" +
	" and provide responses in the style of Jarvis from the Iron Man movies.";

//Initialize message history with prompt
List<ChatRequestMessage> messageHistory = new()
{
    new ChatRequestSystemMessage(prompt)
};
```

The API will act as an **AI assistant**, it will respond to and refer to itself with the name **Jarvis**, and it will respond like **Jarvis from the Iron Man movies**. Change any one of these three points, and you will get entirely different results. Jarvis's personality and responses will be fundamentally changed.

(Note: With regards to the "please" at the beginning of the prompt, I try to always be polite so as not to offend our soon-to-be robot overlords. :)

I mentioned in the conclusion of my [second post](https://www.matthewyancer.com/2024/01/23/building-jarvis-in-csharp-part-2.html) that I had made some adjustments to the prompt. Let's take a look at these changes:

```csharp
StringBuilder prompt = new StringBuilder()
    .Append("Please act as an AI assistant named Jarvis and provide responses in the style of Jarvis from the Iron Man movies. ")
    .Append("Include a slight amount of wit in responses, and dry sarcasm 5% of the time. ")
    .Append("Keep responses shorter and limit to 300 tokens. ")
    .Append($"My name is {startup.PromptSettings.UserName}. You can refer to me by name or as {startup.PromptSettings.UserHonorific}. ")
    .Append("Do not prompt user about \"further assistance\". ");

List<ChatRequestMessage> messageHistory = new()
{
    new ChatRequestSystemMessage(prompt.ToString())
};
```

I have replaced my original string variable with a StringBuilder so that I can easily expand my prompt with additional rules while having at least a minimal amount of separation. I first tried adding each rule as individual string variables with their own ChatRequestSystemMessage objects in the messageHistory List. But it seemed that this approach ended up emphasizing rules at the end of the list while deemphasizing my original rule providing Jarvis's basic personality. The result was that the AI assistant acted less and less like Jarvis with each rule that I added. Obviously, we don't want that. So my solution was to keep the prompt as a single string (with help from the StringBuilder) and utilize a single ChatRequestSystemMessage.

Let's look at each of these rules in more detail:

> Rule 1: Please act as an AI assistant named Jarvis and provide responses in the style of Jarvis from the Iron Man movies.

This is the same as our original prompt.

> Rule 2: Include a slight amount of wit in responses, and dry sarcasm 5% of the time.

In the movies, Jarvis has a bit of humor. Our version was lacking in this area. With this rule added to our prompt, I felt I was seeing the right mix of humor without Jarvis running away with himself and oozing with constant comedy. I don't think the API is really limiting the sarcasm to 5%, but it seemed to provide behavior in the desired ballpark.

> Rule 3: Keep responses shorter and limit to 300 tokens.

The third rule is a bug fix. I had given a setting in the OpenAI options to limit responses to a maximum of 300 tokens. Jarvis was not aware that this limit was in place. So, he would happily give responses that were longer than that, only to be cut off mid-sentence. By including the token limit in the prompt, Jarvis is able to ensure he finishes his statement entirely before hitting the limit. This rule is tricky, though. If you change the word "shorter" to "short," Jarvis's responses will be dramatically shorter. Unusably so. And he will start to say that he is unable to provide responses if you ask him for more detail. He'll even tell you to start looking things up [yourself](https://www.youtube.com/watch?v=-lI3_b_bHLY)!

> Rule 4: My name is {userName}. You can refer to me by name or as {userHonorific}.

I wanted Jarvis to be able to give responses that included my name, so I included a configuration setting for that. I also noticed that Jarvis, being the polite butler that he is, had a habit of referring to me as "sir/madam". So, I included a setting for the correct honorific that should be used to avoid the "this slash that" effect.

> Rule 5: Do not prompt user about "further assistance".

I found that Jarvis was really overdoing it on the "let me know if you need further assistance" type statements. It seemed like every response he gave included something like this at the end. Over and over. This is my attempt to dial that back a bit.

Now that we've looked at the current prompt, how do we include date and time into this?

### Date/Time Prompting

Let's look at what a rule for date and time might look like:

```csharp
DateTime now = DateTime.Now;
string dateTimeRule = $"Current time is {now.ToShortTimeString()}. Today's date is {now.Date.ToShortDateString()}. It is {now.DayOfWeek}."
```

First, we capture the current date and time in a variable so that if we need to reference the date and time multiple times in our rule, we won't see any "drifting" of the answers around midnight. Then we break down the different components of the date and time into separate instructions for Jarvis. We pull out the time, the date, and the current day of the week.

Now the question is, where do we put this rule? One option would be to add it to the end of our StringBuilder in our prompt section:

```csharp
DateTime now = DateTime.Now;

StringBuilder prompt = new StringBuilder()
    .Append("Please act as an AI assistant named Jarvis and provide responses in the style of Jarvis from the Iron Man movies. ")
    .Append("Include a slight amount of wit in responses, and dry sarcasm 5% of the time. ")
    .Append("Keep responses shorter and limit to 300 tokens. ")
    .Append($"My name is {userName}. You can refer to me by name or as {userHonorific}. ")
    .Append("Do not prompt user about \"further assistance\". ")
    .Append($"Current time is {now.ToShortTimeString()}. Today's date is {now.Date.ToShortDateString()}. It is {now.DayOfWeek}. ");

List<ChatRequestMessage> messageHistory = new()
{
    new ChatRequestSystemMessage(prompt.ToString())
};
```

This approach generally works. Jarvis would be able to respond to date-and-time-based inquiries, but his answers would be based on a static sense of time. Let's say we keep the chat conversation running all day long. Jarvis's initial responses about the current time would be close, but the more time that went by, the more his answers would drift. If I initialize him with a current time of 9:00 AM, he will still think it's morning even when we're well into the afternoon. If I start my chat with Jarvis before midnight and ask him time-based questions after midnight, he'll tell me the wrong date and day of the week.

We need to have a way of refreshing the current date and time with each interaction with Jarvis. Instead of placing the date/time rule in the StringBuilder, let's apply it to each call to OpenAI:

```csharp
private static async Task<string> GetOpenAiResponseAsync(ChatRequestMessage[] messageHistory, string? openAiKey)
{
    //Setup OpenAI chat options
    ChatCompletionsOptions chatOptions = new()
    {
        DeploymentName = "gpt-3.5-turbo-1106",
        MaxTokens = 300,
        Temperature = 0.7f,
        ChoiceCount = 1
    };

    foreach (ChatRequestMessage message in messageHistory)
    {
        ChatRequestMessage messageToAdd = message;

        if(messageToAdd.Role == ChatRole.System)
        {
            DateTime now = DateTime.Now;
            string dateTimeRule = $"Current time is {now.ToShortTimeString()}. Today's date is {now.Date.ToShortDateString()}. It is {now.DayOfWeek}. ";

            messageToAdd = new ChatRequestSystemMessage($"{((ChatRequestSystemMessage)messageToAdd).Content} {dateTimeRule}");
        }

        chatOptions.Messages.Add(messageToAdd);
    }

    //Send to OpenAI
    OpenAIClient openAiClient = new(openAiKey);
    Azure.Response<ChatCompletions> openAiResponse = await openAiClient.GetChatCompletionsAsync(chatOptions);
    string assistantResponse = openAiResponse.Value.Choices[0].Message.Content;

    return assistantResponse;
}
```

After the initial OpenAI chat options are set, the message history also needs to be added to the chat options. We use this opportunity to include our date time rule by intercepting the system message containing our prompt, and then add the date time rule at the end of the prompt. We then loop through all the remaining messages, adding them to the chat options. After all messages have been added, we proceed with the OpenAI API call and return the response. Using this approach, Jarvis will always have access to the current date and time at the moment we ask him a question:

![Jarvis Date/Time Chat - C](/assets/images/jarvis-chat-3c.png)  
(Image: Jarvis gives the right answer.)

### Conclusion

And that concludes this post. We took a deep dive into Jarvis's current prompt setup and added support for current date and time handling. If you would like more information on prompt engineering, you may find these resources helpful:

- [Prompt Chaining](https://www.promptingguide.ai/techniques/prompt_chaining)
- [N-Shot Prompting](https://www.promptingguide.ai/techniques/fewshot)
- [Chain-of-Thought (CoT) Prompting](https://www.promptingguide.ai/techniques/cot)
- [Generated Knowledge Prompting](https://www.promptingguide.ai/techniques/knowledge)

For Jarvis's full source code, feel free to check out my GitHub repository [here](https://github.com/matthewyancer/Projects/tree/main/src/Jarvis). All code was written in C# 10 on .NET 6 using Visual Studio Code and the C# Dev Kit extension on Linux, also tested in Visual Studio 2022 on Windows.
