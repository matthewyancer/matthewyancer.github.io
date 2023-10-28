## C# and .NET News Updates

Some news updates in the C# and .NET space that have caught my attention over the last few months:

### C# Dev Kit

Earlier this month, the C# Dev Kit for Visual Studio Code, previously announced back in [June 2023](https://devblogs.microsoft.com/visualstudio/announcing-csharp-dev-kit-for-visual-studio-code/), was [released](https://devblogs.microsoft.com/dotnet/csharp-dev-kit-now-generally-available/). With all of the attention Microsoft has been giving lately to cross-platform .NET for Windows, MacOS, and Linux, it has always been amazing to me that there wasn't a good first-party solution for developing in .NET on MacOS and Linux before. Of course, there are 3rd-party options, such as [JetBrains Rider](https://www.jetbrains.com/rider/) or [MonoDevelop](https://www.monodevelop.com/) (I see you [Visual Studio for Mac](https://adtmag.com/articles/2017/05/10/vs-for-mac.aspx)), but where was the Microsoft solution?

I've been kicking the tires a bit on the C# Dev Kit. It is interesting to have such a light environment for .NET. I have used every version of Visual Studio from the original Visual Studio .NET Beta back in 2001 to now. I've never seen an installation go so quickly and take up such little space. I'm running it on my favorite linux distro, [Ubuntu MATE 22.04](https://ubuntu-mate.org/), using a [low-end laptop](https://www.bestbuy.com/site/hp-14-laptop-intel-celeron-4gb-memory-64gb-emmc-snowflake-white/6499749.p?skuId=6499749) with an upgraded RAM stick. The performance of this setup is surprisingly good.

So far, I've tried out the C# Dev Kit basics:
- Project Templates
- File Templates
- Building Code
- Setting Breakpoints and Stepping Through Debugger
- Intellisense
- Code Snippets
- XML Comments
- Code Navigation, such as Go To Definition and Find All References

It's cool seeing the new simplified Solution Explorer inside VS Code. I'm also curious to try out the automated unit testing integration and Copilot AI. Let's be clear: this is a very stripped down experience. Does it cover enough of what's needed to be productive on a daily basis? The jury is still out.

For more on the C# Dev Kit, Scott Hanselman has an introductory video [here](https://www.youtube.com/watch?v=6BNtIxW0-xQ).

### WCF

As Microsoft has been focusing on cross-platform capabilities, features that don't exist across all environments have been left on the cutting room floor. One feature that has been impacted is WCF. I don't know if Microsoft realizes how big of a loss this is. (I'll touch on this in a future post.) It's good to see that they have been slowly adding WCF back to current versions of .NET.

Over the last several months, WCF has been seeing some significant improvements. Client support for calling WCF/CoreWCF has been added with [System.ServiceModel 6.0](https://devblogs.microsoft.com/dotnet/wcf-client-60-has-been-released/). Work on [new transports](https://github.com/CoreWCF/announcements/issues/15), RabbitMQ, Apache Kafka, MSMQ, and NetNamedPipes, is in progress with [CoreWCF 1.4.0](https://www.infoq.com/news/2023/09/corewcf-140-released/). They are also working on an equivalent NetNamedPipes feature for Linux using Unix Domain sockets in CoreWCF 1.5.0.

### .NET 8 and C# 12

.NET 8 is scheduled to be released on November 14, 2023. This is a Long-Term Support (LTS) release. Take a look [here](https://modlogix.com/blog/net-8-features-and-release-date-what-to-expect/) and [here](https://www.infoworld.com/article/3704992/the-key-new-features-and-changes-in-net-8.html) for a summary of changes. This release of .NET will also come with C# 12; check [here](https://dev.to/techiesdiary/c-new-features-and-improvements-in-c-12-3n3f) for changes.

### .NET Conf 2023

Microsoft is hosting [.NET Conf 2023](https://www.dotnetconf.net/), their biggest .NET virtual event, on November 14–16, 2023. This free event will focus on the release of .NET 8. In addition to coverage on .NET 8, C# 12, and the new C# Dev Kit for Visual Studio Code, it's looking like all of the important .NET technologies and topics will be covered, based on the [conference agenda](https://www.dotnetconf.net/agenda).

Shaping up to be an exciting fall in the .NET space!
