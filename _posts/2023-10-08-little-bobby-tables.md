## Little Bobby Tables

Here's a great comic touching on injection attacks, from XKCD:

![Comic: XKCD Exploits of a Mom](https://imgs.xkcd.com/comics/exploits_of_a_mom.png)  
(Image from [XKCD](https://xkcd.com/327/))

I always use this comic to kick off discussions with young developers on security vulnerabilities. The third panel of the comic depicts a database injection attack. An injection attack takes advantage of code that is running in a system by supplying it with additional unexpected rogue code mixed into input data. When running this ficticious student's name in a database query, it completes the intended SQL statement that is currently running with the *apostrophe, parentheses, and semicolon*. Then it starts a new SQL statement to delete all records from the Students table. Followed by a *dash dash* to comment out any remaining SQL code from the system after that so that the statements run successfully without error.

Of course, for this bit of SQL to work correctly, there would have to be a Students table. Attackers would use some other means of determining table names, such as attacking a well-known system with an understood table layout. Or they could have an additional attack to determine table names. To prevent an attack like this from happening, you would need to provide some type of guarding to ensure that executable code is not embedded in your data or use a technique to prevent the execution of code within the data, such as by using a parameterized query.

The next stop when reviewing security vulnerabilities is looking at the [OWASP Top 10](https://owasp.org/www-project-top-ten/), which is currently (as of the 2021 update):

1. Broken Access Control
2. Cryptographic Failures
3. Injection
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable and Outdated Components
7. Identification and Authentication Failures
8. Software and Data Integrity Failures
9. Security Logging and Monitoring Failures
10. Server-Side Request Forgery

It's hard to believe that for my entire career, Injection has been in the top ten. At least it has moved down to #3 from the #1 slot in the previous revision. If you are a software developer and you are not familiar with this list and how to prevent these vulnerabilities, it is worth your time to review it.

Here's an additional listing of [30 tips for software developers to enhance software security](https://codesigningstore.com/tips-for-software-developers-to-enhance-software-security) which touches on some good topics.

And this is just the beginning. What are some software development security best practices that you follow?
