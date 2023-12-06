## Test Doubles

Picture this: your hard-working, disciplined software developers are diligently writing automated unit tests for all of their code [as they should](https://www.matthewyancer.com/2023/10/24/got-tethics.html#:~:text=comprehensive%20automated%20test%20suite). And then they need to write some tests for code that integrates with one of these scary-looking API calls:

```csharp
crm.SendSmsMessageToAllCustomers(message);

payroll.GiveAllEmployeesBonus(amount);

powerGrid.ShutdownCity();

military.LaunchTheBigOne();
```

Calling any one of these could have real-world ramifications—financial, customer relationships, or otherwise. So, this code should absolutely not be executed as part of a test, let alone as a set of automated unit tests that are executed many times per day by many developers and your automated build system. So, what do you do in this situation?

Enter the *Test Double*.

![Lucas Lee's Stunt Doubles](/assets/images/lucas-lee-stunt-doubles.webp)  
(Image from [here](https://scottpilgrim.fandom.com/wiki/Lucas_Lee%27s_Stunt_Doubles))

Just like a Hollywood actor's [stunt double](https://people.com/movies/actors-and-their-stunt-doubles-photos/), who steps in for the actor when its time to film something dangerous, a test double steps in for integrated calls that would be difficult or impossible to test normally. *Because if you were to execute one of the above methods in a unit test, you would be as unemployeed as a Tom Cruise stunt double.* For example, we don't want to repeatedly send test SMS messages to all of our customers every time the test suite runs. So instead, we use a fake version of our SMS API, which can log what has been "sent" and keep track of how many messages have "gone out" but doesn't actually send anything to the customers. This ensures interaction with the API is being done correctly, but without the high cost (and customer relationship nightmare) of sending millions of messages over and over.

```csharp
[TestMethod]
public void SendSmsMessageToAllCustomers_WithEntireCustomerList_MillionMessagesSent()
{
    //Arrange
    ISmsApi smsApiFake = new SmsApiFake();
    string testMessage = "This is a test message!";
    int expected = 1000000;

    //Act
    ICrmSystem target = new CrmSystem(smsApiFake);
    int actual = target.SendSmsMessageToAllCustomers(testMessage);

    //Assert
    Assert.AreEqual(expected, actual);
}
```

Somewhere else, there can be testing of sending a few actual SMS messages to ensure integration with the real 3rd-party API is functioning. (And tests for the throttling architecture to spread out the sending of a million messages so that they all actually go through.)

A key component to making this technique work is the use of interfaces. In order to substitute the SMS API with a fake version for testing, the real SMS API and the fake one must adhere to the same contract. In the example above, this contract is called *ISmsApi*. By using an [interface](https://www.matthewyancer.com/2023/10/03/the-pizza-ordering-interface.html), the actual implementation of the code can vary, but the interactions with the contract will remain the same.

For more information on test doubles, Martin Fowler has some good write-ups [here](https://martinfowler.com/bliki/TestDouble.html) and [here](https://martinfowler.com/articles/mocksArentStubs.html).
