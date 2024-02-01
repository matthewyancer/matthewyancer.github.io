## Building Jarvis in C#, Part 1: Conversational Chat

I have always found the Iron Man movies to be inspiring from an engineering perspective. It's not unusual for me to have one of these movies playing in the background while developing. And I've often wondered what it would be like to have my own Jarvis assistant helping me while I work. The YouTube algorithm suggested a [video](https://www.youtube.com/watch?v=BEw5EFqCCEI) to me recently on creating a version of Jarvis using Python and the OpenAI API. Taking inspiration from this, let's look at creating Jarvis in C# using OpenAI.

![Jarvis Chat](/assets/images/jarvis-chat-1.png)

### The Chat Loop

The conversation with Jarvis will be implemented using an infinitely repeating loop. Input will be gathered from the user, chat information will be sent to OpenAI to generate Jarvis's response, the response will be given back to the user, and this will be repeated over and over until the user terminates the session. As we loop through the chat, we will also keep track of the history of the conversation. The OpenAI API is stateless and doesn't remember previous interactions, so you must remind it of what has been previously discussed to keep the conversation moving forward. 

Here is an outline of how this looks:

```csharp
while (true)
{
    //Get user input

    //Add user input to message history

    //Setup OpenAI chat options

    //Send to OpenAI

    //Add assistant response to message history

    //Output assistant response
}
```

To end the chat session, the user will either hit ctrl-c or close the console window.

Now let's look at how to fill in each of these areas, starting with input and output.

### Input and Output

For the first version, we'll be keeping input and output simple. The console will be used for reading in typed input from the user, and then the console will be used to output Jarvis's responses as text to the screen. In later versions, these areas of the code could be upgraded with speech-to-text and text-to-speech interfaces.

To get user input, we'll do the following:

```csharp
//Get user input
string? userInput = null;
while (userInput == null || userInput == string.Empty)
{
    Console.Write(">> ");
    userInput = Console.ReadLine();
}
```

We continually loop on inputs until we have some actual text from the user.

And for Jarvis's response output, we'll make a simple Console.WriteLine call:

```csharp
//Output assistant response
Console.WriteLine(assistantResponse);
Console.WriteLine();
```

Easy enough. Ok, now on to the integration with the OpenAI API.

### OpenAI Integration

Before we proceed, you'll need to obtain an OpenAI API key if you don't already have one. You'll also need to ensure you have non-expired credit in your account. (Note: trial credit expires after 3 months, and purchased credit expires after 1 year.) You can reference [this video](https://www.youtube.com/watch?v=UO_i1GhjElQ) if you need help with how to set them up.

For calling OpenAI from C#, we'll be using the Azure.AI.OpenAI nuget package, which is available [here](https://www.nuget.org/packages/Azure.AI.OpenAI). You can also add it to your project from the command line using the following command:

```plaintext
dotnet add package Azure.AI.OpenAI --version 1.0.0-beta.12
```

Despite having "Azure" in the name, you can also use this package to directly connect to the OpenAI API from your local machine without Azure in the mix. Please note that this library is currently in beta and could have changes prior to its final release. I ran into this exact issue while referencing [this video](https://www.youtube.com/watch?v=0qmF2-f7TgA) which is based on the beta 5 version. The libary syntax has undergone major changes between beta 5 and beta 12 that I had to account for.

Ok, now that we have an OpenAI API key and we have the Azure.AI.OpenAI nuget package, let's integrate them with our chat loop.

First, we'll need to set up the OpenAI chat options:

```csharp
//Setup OpenAI chat options
ChatCompletionsOptions chatOptions = new()
{
    DeploymentName = "gpt-3.5-turbo-1106",
    MaxTokens = 300,
    Temperature = 0.7f,
    ChoiceCount = 1
};

foreach (var message in messageHistory)
    chatOptions.Messages.Add(message);
```

This configures the latest version of the GPT 3.5 Turbo model, limits the number of tokens in the response to 300, sets the temperature to a value of 0.7, and limits the number of response choices to 1. Feel free to experiment with other options here.

After the options are set, we add the messages that are part of the conversation history up to this point so that the stateless OpenAI API can base its response on what has been discussed. We'll look at how to maintain the conversation history later.

Next, let's make the actual call to OpenAI:

```csharp
//Send to OpenAI
OpenAIClient client = new(startup.ApiSettings.OpenAiKey);
Azure.Response<ChatCompletions> openAiResponse =
	await client.GetChatCompletionsAsync(chatOptions);
string assistantResponse = openAiResponse.Value.Choices[0].Message.Content;
```

The OpenAI client is initialized with the OpenAI key that is passed in from the appsettings.json file. Then a call is made to OpenAI to obtain a response based on the passed-in chat options. Once we have the response object, we extract the response string.

For the final step, let's look at how to maintain the conversation history.

### Maintaining Conversation History

In order to keep track of the conversation's history, we'll need a place to store it. We'll use a simple List<T> sitting outside our chat loop for this purpose. We'll also initialize our conversation with a prompt so that the responses we receive actually sound like Jarvis:

```csharp
string prompt = "Please act as an AI assistant named Jarvis" +
	" and provide responses in the style of Jarvis from the Iron Man movies.";

//Initialize message history with prompt
List<ChatRequestMessage> messageHistory = new()
{
    new ChatRequestSystemMessage(prompt)
};
```

The above lines are added before our chat loop. Note that the prompt uses the "System" role, which is specified in the ChatRequestSystemMessage object name.

Next, we'll need to add the user input and Jarvis's responses to the history as part of the chat loop:

```csharp
//Add user input to message history
messageHistory.Add(new ChatRequestUserMessage(userInput));

//Add assistant response to message history
messageHistory.Add(new ChatRequestAssistantMessage(assistantResponse));
```

User input messages use the "User" role, specified by the ChatRequestUserMessage object name. Jarvis's responses use the "Assistant" role, specified by the ChatRequestAssistantMessage object name.

### Conclusion

And that's it! You may enjoy playing around a bit with the prompt and some of the other settings, such as temperature, to see how it impacts the responses you get.

For the full source code, feel free to check out my GitHub repository [here](https://github.com/matthewyancer/Projects/tree/main/src/Jarvis). All code was written in C# 10 on .NET 6 using Visual Studio Code and the C# Dev Kit extension on Linux, also tested in Visual Studio 2022 on Windows.
