## Types of Automated Unit Tests

Unit testing is a practice for validating the correctness of sections, known as units, within a software system. A tester can manually perform it using a client that allows executing a unit of the system while following a defined set of steps to validate its behavior. Or, test code can be written to [automate the process](https://xkcd.com/1205/) of validating units of the production code, known as automated unit testing. These automated tests are typically written with a unit testing framework such as [NUnit](https://nunit.org/), [MSTest](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-mstest), or [JUnit](https://junit.org/junit5/). Having a suite of automated tests can be very useful. They often run so quickly that you can retest an entire system with each change to the code in a fraction of the time that it would take to manually test a single unit.

For development teams that are new to developing automated unit tests, there can be a significant learning curve to figure out how to structure the tests. To help with this, I will describe four general types of automated tests:

- **Logic/Calculation**—for testing components within your system that contain logic, calculations, or rules. These are the simplest tests to write and should be where your team focuses its early efforts. Use a [black](https://en.wikipedia.org/wiki/Black-box_testing)-[box](https://www.guru99.com/black-box-testing.html) [testing](https://softwareengineering.stackexchange.com/questions/362746/what-is-black-box-unit-testing) technique here. Pass in various input scenarios and validate the expected outputs. Avoid writing too many tests that validate nulls, zeros, minimum values, maximum values, and empty strings. A few of these tests are okay to have, but they are often low-value. Focus on inputs that have business meaning. Account for inputs that trigger boundary conditions.

- **Resource Access**—for testing units whose responsibility is to provide access to an underlying resource within your system, such as a database or a file. For these tests, you need to ensure a clean starting state for the resource so that repeated test executions are consistent. You will then need to populate it with known values. Then set up your test scenario, conduct the test, and validate. Then roll back the resource to the known value state between each test. Finally, clean up the resource at the end of the test run so that it's ready for the next execution.

- **Orchestration**—for testing units whose responsibility is to coordinate and integrate different modules within your system. These units require a [white](https://en.wikipedia.org/wiki/White-box_testing)-[box](https://www.guru99.com/white-box-testing.html) [testing](https://www.browserstack.com/guide/white-box-testing) pattern. These tests confirm interactions between different modules in the system. Were the correct dependencies called? Were they called in the correct order? Were they called the correct number of times? Did branching paths lead to the expected interactions? These tests typically require the use of a mocking framework, such as [Rhino Mocks](https://hibernatingrhinos.com/oss/rhino-mocks) or [JMock](http://jmock.org/), to fake dependencies so that you are only testing the unit under test and not doing a full integration test.

- **Integration**—strictly speaking, integration tests are not *unit* tests, though they can be automated using a unit testing framework. These tests typically execute multiple modules together across all layers of the system. They can require a lot of setup and configuration. You may also need to set resources to known states (and clean them up), just like with resource access tests. If one of these tests fails, it can be difficult to pin down where the issue is. Limit the number of these types of tests in your testing suite. These tests tend to follow more of a [gray](https://en.wikipedia.org/wiki/Gray-box_testing)-[box](https://www.guru99.com/grey-box-testing.html) [testing](https://www.geeksforgeeks.org/gray-box-testing-software-testing/) pattern, using a hybrid of black-box and white-box techniques.

Assume that 3rd-party services have been tested thoroughly by the 3rd party. Don’t try to test their internals, only your connectivity to their service. Have some tests to confirm connectivity. Then have the rest of your tests be white-box orchestration tests where you mock your dependency on the 3rd-party service and validate what your system would do when it receives certain responses.

Please note that if you are trying to add automated unit tests to a system that wasn't designed for testing, you may have an uphill battle due to the overall structure of the system and dependencies throughout the code. I recommend [Michael Feathers book *Working Effectively with Legacy Code*](https://www.amazon.com/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052) for tips on how to refactor a codebase for automated unit testing.