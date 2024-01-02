## Announcing JustTooFast XML Library

Happy New Year! As part of the second release of the JustTooFast open-source project, I'm pleased to announce the immediate availability of the **JustTooFast.Xml library**. Developers can programmatically create XML documents using this library.

The source code is hosted on GitHub at: [https://github.com/JustTooFast/JustTooFast](https://github.com/JustTooFast/JustTooFast). The project is licensed under the [Apache License, version 2.0](https://www.apache.org/licenses/LICENSE-2.0).

Below is a summary of the updates available in this release.

Adding first version of the XML library:

- Generates strings for XML Files and XML Snippets.
- Uses an intuitive builder interface for programmatically specifying XML structure.
- Includes support for optional XML Declaration, Root Element, Nested Child Elements, and Attributes.
- Includes basic XML format validation rules.

Minor updates to the BidFast library:

- Removed 'Generate' method stub from generated Declaration classes to allow for implementation flexibility.
- Added 'Validate' method stub to generated Declaration classes to allow for implementing validation rules.
- Added partial keyword to the generated Info classes to allow for extensions as necessary.
- Implemented simple validation rules within SampleXml library.

A suite of 125 automated unit tests is included in this release. The code is written in C# 10 on .NET 6.

This release was entirely developed using Microsoft Visual Studio Code and the C# Dev Kit extension on Linux. And tested for cross-platform use on Linux and Windows. In addition to the x64 CPU architecture, the arm64 CPU architecture has been tested using a Raspberry Pi 400.

Cheers and best wishes,  
Matthew Yancer
