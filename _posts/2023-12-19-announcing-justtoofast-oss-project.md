## Announcing JustTooFast OSS Project

Today, I'm pleased to announce the first release of my new personal open-source software project, **JustTooFast**, which will focus on libraries and tools for boosting developer productivity.

The source code is hosted on GitHub at: [https://github.com/JustTooFast/JustTooFast](https://github.com/JustTooFast/JustTooFast). The project is licensed under the [Apache License, version 2.0](https://www.apache.org/licenses/LICENSE-2.0).

Included in this first release is a library and tool designed for accelerating the development of code generation libraries, named BidFast. It uses a simple domain-specific language (DSL) to quickly generate the repetitive portions of **B**uilder, **I**nfo, and **D**eclaration classes, which can be used in combination to programmatically produce markup and programming language code using an intuitive interface. This tool will be used for further development and expansion within the JustTooFast project and is being made immediately available to the community.

A sample generated library and a suite of 80 automated unit tests are included. The code is written in C# 10 on .NET 6.

This first release was entirely developed using Microsoft Visual Studio Code and the C# Dev Kit extension on Linux (Shout out to [Ubuntu MATE 22.04.3 LTS Jammy Jellyfish](https://ubuntu-mate.org/) — you've become my daily driver). And tested for cross-platform use on Linux and Windows. In addition to the x64 CPU architecture, the arm64 CPU architecture has been tested using a Raspberry Pi 400.

As a long-time user of open source software, I'm glad for the opportunity to give back in this small way. [Code generation](https://en.wikipedia.org/wiki/Code_generation) and [metaprogramming](https://en.wikipedia.org/wiki/Metaprogramming) are passions of mine. I'm excited to share them with all of you.

Cheers and best wishes,  
Matthew Yancer
