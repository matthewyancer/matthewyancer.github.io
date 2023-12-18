## Cross-Platform .NET Notes

For quite some time, I've been intrigued by the idea of a more stripped-down, lightweight development environment for C# and .NET, possibly even working from a command line. Enter Visual Studio Code and the new C# Dev Kit extension. Seeing that this environment was equally available on Windows and Linux, it seemed like a good time to test out cross-platform .NET development as well. Below, you'll find some learnings I've encountered along the way.

### .NET Core only

.NET on Linux and MacOS means you'll be using .NET Core (.NET 6.0, 7.0, or 8.0). .NET Framework is Windows only, though I should note that .NET 4.8.1 has added support for [Arm64](https://devblogs.microsoft.com/dotnet/announcing-dotnet-framework-481/) on Windows 11. If you are using Ubuntu, you may find the [following](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu) [links](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-2204) to be useful for setting things up. On Ubuntu 22.04 LTS, .NET 7.0 and 6.0 are available from the Ubuntu feed, but .NET 8.0 is not. I did try adding the Microsoft feed in order to get access to .NET 8.0 and I ran into some issues with Visual Studio Code and C# Dev Kit not being able to find some portions of the .NET environment no matter what I tried. The issues vanished once I switched back to .NET 7.0 on the Ubuntu feed. Hopefully, the Microsoft feed will get this issue sorted out in a newer version. Ubuntu feed for version 23.10 also has support for .NET 8.0, so perhaps the issue doesn't exist there.

### String and File Line Endings

Someone, somewhere, thought it would be a [great idea](https://stackoverflow.com/questions/419291/historical-reason-behind-different-line-ending-at-different-platforms) to have different ways to represent line endings on different platforms. On Windows machines, line endings typically use carriage return followed by line feed (CRLF), or in C#, "\r\n". On Unix machines, such as Linux or modern versions of MacOS, line endings are a line feed (LF) only, or in C#, "\n". The [Environment.NewLine](https://learn.microsoft.com/en-us/dotnet/api/system.environment.newline?view=net-7.0) property can be used to retrieve the line ending string defined for the current environment. And routines such as [StreamWriter.WriteLine](https://learn.microsoft.com/en-us/dotnet/api/system.io.streamwriter.writeline?view=net-7.0) or [StringBuilder.AppendLine](https://learn.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.appendline?view=net-7.0) also make use of the Environment.NewLine string, automatically switching as needed for the current environment. So, everything's good, right?

Almost. C#'s [verbatim string literals](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/verbatim) do not make use of Environment.NewLine. Whatever format your editor was set to (LF or CRLF) is what will be used for the verbatim string literal every time you press the enter key. It appears that Visual Studio uses LF for C# files on Windows by default, and VS Code on Linux also uses LF. If you compare a verbatim string literal that uses LF with a StringBuilder string that uses CRLF automatically, you will find that they don't match. Visualizers for MSTest Assert statements will show [no apparent difference](https://twitter.com/TechJuicePk/status/1149299225508945920) in the strings because they don't render the actual line-ending characters. You have to set break-points on the specific variables in the debugger to see the actual "\n" vs. "\r\n" in the strings.

Some other fun line-ending trivia:

1. Git for Windows can also have some interesting interactions in this area, as the recommended default is to have Git automatically convert line endings from LF to CRLF on Windows and then back to LF when checking in. I'm sure there will be no annoying side effects from this.

2. Linux shell scripts don't like CRLF line endings and will throw errors.

3. Changing Visual Studio's line ending mode doesn't change existing line endings in a file. If you do this, you will end up with mixed line-endings. Visual Studio will complain about this when you open the file at another time.

4. Notepad++ has a wonderful feature that can convert all line endings in a file to a specific type. Go to Edit -> EOL Conversion and pick from Windows (CR LF) or Unix (LF). There is also Macintosh (CR), which is just a '\r'; keep in mind that this is for classic versions of the Macintosh operating system. If you are on Mac OS X or modern MacOS, then you are on a Unix system, and LF is your friend.

### Directory Separator Characters

Similar to the difference in handling of line endings between Windows and Unix platforms, there is also a difference in [type of slash](https://superuser.com/questions/176388/why-does-windows-use-backslashes-for-paths-and-unix-forward-slashes) used for folder structures on the platforms. On Windows machines, backslashes (\) are used to separate folder names. On Unix machines, such as Linux or modern versions of MacOS, forward slashes (/) are used. The [Path.DirectorySeparatorChar](https://learn.microsoft.com/en-us/dotnet/api/system.io.path.directoryseparatorchar?view=net-7.0) field can be used to determine the correct character to use for the current environment.

This technique works great if you are specifying folder structures from within C# code, but Path.DirectorySeparatorChar does not help with folder references within project files. Fortunately, if you are specifying a folder structure within an ItemGroup, MSBuild will happily accept a backslash on both Windows and Linux. For example:

```xml
<ItemGroup>
  <Compile Include="..\SolutionInfo.cs" Link="Properties\SolutionInfo.cs" />
  <Compile Include="Properties\AssemblyInfo.cs" />
</ItemGroup>
```

...will work fine on both platforms.

MSBuild variables such as $(ProjectDir) and $(OutputPath) will automatically switch between the proper directory separator characters as needed. But any system commands (such as for a pre-build or post-build event) will have to account for the differing directory separator characters manually.

Speaking of which...

### Pre-Build Events

Any external system commands that you execute as part of a pre-build (or post-build) event must account for the underlying system that they will be running on. In addition to the differing directory separator characters mentioned above, Windows and Unix platforms have differing ways of performing other operations, such as deleting files, for example ("del" in Windows, "rm" on Unix platforms). You can split these system-specific operations into two sections within your project file that will run on their specific platforms, like this:

```xml
<Target Name="PreBuild" BeforeTargets="PreBuildEvent" Condition=" '$(OS)' == 'Windows_NT' ">
  <Exec Command="del /f /q &quot;$(ProjectDir)Output\*.gen.cs&quot;" />
</Target>

<Target Name="PreBuild_unix" BeforeTargets="PreBuildEvent" Condition=" '$(OS)' == 'Unix' ">
  <Exec Command="rm -f &quot;$(ProjectDir)Output/*.gen.cs&quot;" />
</Target>
```

Notice that the "Condition" specifies which environment will be used to run the command. (In this case, Linux and MacOS which are both recognized as "Unix", will use the same command. If you need to execute something different on Linux and MacOS, see [here](https://jeremybytes.blogspot.com/2020/05/cross-platform-build-events-in-net-core.html).) Also notice that I have specified different "Names" for each environment. When I tried to use the same name, MSBuild could only see whichever definition was defined last (regardless of the "Condition"), resulting in a script that works on one environment and [not the other](https://www.youtube.com/watch?v=RgI0pbnJtYo&t=14s).

If you are calling an executable that has been built as part of the current build process, on Windows an executable file ending in ".exe" will be produced, but on a Unix platform there won't be one. Instead, there will be an executable file with no extension. Or, there is an alternative call style that will also work on both platforms:

Windows only:

```plaintext
MyApp.exe
```

Unix:

```plaintext
MyApp
```

Both Windows and Unix Platforms:

```plaintext
dotnet MyApp.dll
```

*NOTE: If you need to pass arguments to your application when running in this alternate style, you must put " -- " before the argument list. For example:*

```plaintext
dotnet MyApp.dll -- arg1 arg2
``` 

Now onto some Visual Studio quirks. If you attempt to edit Pre-Build events from within Visual Studio, you will be greeted by this nice looking text box that has the appearance of being multi-line.

![Visual Studio: Pre-Build Event Dialog](/assets/images/vs-pre-build-event.png)

And sure enough, Visual Studio will let you enter multiple commands into the box. But when you save, exit, and come back, it will have put all of the commands into a single Exec statement in the project file. And subsequent viewing will be single-line. It seems that Visual Studio really wants you to use a single call to a batch file in place of multiple Exec statements, should you have the need. Note that multiple Exec statements will run just fine, but only the first Exec statement will display in the Visual Studio dialog. One other little gotcha, the Visual Studio dialog will only display Pre-Build event for the the Target section that has been specifically labeled with the name "PreBuild". Other sections, such as "PreBuild_unix" from my above example, will not display on screen. And if you change the name of "PreBuild" to something like "PreBuild_win", it will no longer display on screen either.

### Unit Testing

While working with MSTest in C# Dev Kit, I noticed some general flakiness with automatic unit test discovery in the testing pane. Note that you have to build your projects before tests will appear in the testing pane, which is understandable. But I noticed that not all tests reliably appear, especially when you are actively adding additional tests. Rebuilding the code base doesn't help. Sometimes new tests will be discovered upon execution of the other tests, but the new tests are not included in the execution. You have to run the tests again to include all of them. Sometimes I couldn't get tests to appear, no matter how many times I rebuilt. The only solution was to close Visual Studio Code and reopen. And then, of course, rebuild the solution at the prompting of the testing pane yet again. Finally, the tests would appear. It's a bit fiddly, but given how new this platform is, I'll forgive it for now. Lastly, if I'm being very quibbly, the displayed number of executed tests seemed to display random numbers at times that had no correlation to the number of tests actually executed. Please note that I was primarily working on Linux. I don't know if the testing pane behaves similarly on Windows.

### Raspberry Pi

Visual Studio Code is also available for Linux running on the Raspberry Pi. If you are running a [64-bit](https://ubuntu-mate.org/download/) [build](https://www.raspberrypi.com/software/operating-systems/) of Linux, then you can also install the C# Dev Kit extension from within Visual Studio Code. I can verify it works great on the Raspberry Pi 400, offering an inexpensive way to test .NET on Arm64 architecture. Please note that there are Visual Studio Code builds for 32-bit as well, but only a subset of the necessary C# extensions are available on 32-bit.

### Conclusion

And that's all for today. Generally, I have to say I've quite enjoyed working with Visual Studio Code and the C# Dev Kit on Linux. If templating within the C# Dev Kit can be made a little more robust in terms of quantity and file contents, extension performance can be improved, and unit test discovery can be sorted out, then I see the makings of a very enjoyable and productive environment. The lightweight environment lends itself to higher focus and a feeling of being closer to the metal. I really appreciate being able to easily edit project files without having to dance around an IDE. It feels fresh, new, and simple. I can only imagine it's like a writer using a distraction-free writing tool such as Scrivener, FocusWriter, a Freewrite typewriter, or a [vintage Mac](https://www.alexroddie.com/2013/10/two-months-writing-with-vintage-mac/). Toggling back to Visual Studio felt so much heavier with too many panes, dialogs, settings screens, etc.

What cross-platform .NET issues have you encountered?
