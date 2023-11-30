## Don't Repeat Yourself

Someone at Microsoft seems to be overly bothered by repetition.

Take this C# variable declaration:

```csharp
Patient p = new Patient();
```

This statement declares an object named "p" of type Patient and assigns a new instance of the Patient class to it. Simple enough. But there's that pesky repetition of "Patient". A feature was released back in 2007 with version 3.0 of C# that allowed a developer to remove this repetition like so:

```csharp
var p = new Patient();
```

Everyone's happy now, right? Well, actually, no.

Using the var keyword reminded a lot of developers of VBScript's [variant](https://www.csidata.com/custserv/onlinehelp/VBSdocs/VBS6.HTM) data type, which could hold any type of data but was not [strongly typed](https://stackoverflow.com/questions/3376252/what-are-the-benefits-and-drawbacks-of-a-weakly-typed-language). Var and variant both start with "var", after all. And it sure seems like var can be anything:

```cs
var b = new Bird();
var c = new Cat();
var d = new Dog();
```

But it turns out that using var is just [syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar) for the developer. The compiler still treats the var as the referenced type. So what actually gets compiled is:

```csharp
Bird b = new Bird();
Cat c = new Cat();
Dog d = new Dog();
```

Var is, in fact, strongly typed. Everyone's happy now, right? Well, actually, no.

Developers love using var because it makes it faster to type code. Not because of the number of characters they are typing (Intellisense/tab completion in Visual Studio often shortens the number of characters you are typing for a data type to just a few keystrokes), but because they don't have to think about the data type. They can focus on what they're going to name the variable. It also makes refactoring the code faster because there is less to change when renaming types (although the IDE can rename everything at once, so I don't understand this argument). But as a code reviewer, it's awful to read through lots of code littered with var. You have to chase down what was being assigned to the variable to see its type, which is a pain with long lines of code. And what if you have a line of code where it's not obvious what data type is being used?

```csharp
var myFancyVariable = SeriousObjectFactory.GetTheNecessaryThing();
```

Yes, I know you can drag the mouse over and hover on the code to see the return type *while in Visual Studio*. But when reading through code, lots of mouse hovering is fatiguing (*"Wait, what type was that variable again?"*). And hovering doesn't work if you are looking at the code in a different text editor, source code repository, or diff tool. Good variable and method naming can help, but sometimes there are types in a system with similar names. And naming skills vary across developers.

I will also add that, from a philosophical standpoint, using the data type in place of var allows you to state a contract of sorts. This variable must be able to support the operations of the declared type. It's so important that I'm going to state right here in this variable declaration that these are the operations I expect as I go on to use this variable throughout the rest of this section of the code. In the above code snippet, if someone changes the return type of "GetTheNecessaryThing()", I won't get a compiler error on that line. It will pop up on some other line, or it may not pop up at all (perhaps this is why developers feel like var is weakly typed). If instead, I declare my type like this:

```csharp
FancyContract myFancyVariable = SeriousObjectFactory.GetTheNecessaryThing();
```

Now, if someone changes the return type of "GetTheNecessaryThing()", I will receive the compiler error right here on this line of code. Note: I have no problem with dynamic typing in languages, but when I'm using a statically typed language, I expect that the static typing isn't being defeated.

So, how can we remove the data type repetition while avoiding the var usage debates? C# 9.0 to the rescue with the **target-typed new** feature. Remove the repetition by flipping the data type from the constructor invocation on the right-hand side to the variable declaration on the left-hand side, like this:

```csharp
Patient p = new();
```

Now you get the readability of the data type next to the variable name and no repetition.

I was recently testing [Visual Studio Code and the new C# Dev Kit](https://www.matthewyancer.com/2023/10/21/csharp-and-dotnet-news-updates.html), and it was giving some suggestions on how I could improve the structure of my code: *'new' expression can be simplified ([IDE0090](https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/style-rules/ide0090))*. Clicking on Quick Fix, it changed this code:

```csharp
List<string> result = new List<string>();
```

To this:

```csharp
List<string> result = new();
```

I *think* I'm fine with target-typed new as a language feature. Although I will say, it's spooky to me that changing the data type on the left causes an entirely different constructor to be executed on the right without any change to the code on that side. But I'm surprised that Microsoft went to the trouble to write an IDE rule to tell me that I should be using this language feature. Does the lack of data type repetition really make this style of writing the code that much better? Is it worth the confusion introduced to less experienced developers by having three different ways to write the same thing? I really wonder sometimes about Microsoft's [changes](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/instance-constructors#primary-constructors) to the C# language. I'm also not sure that this level of repetition is what is meant by the [Don't Repeat Yourself (DRY) Principle](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself).
