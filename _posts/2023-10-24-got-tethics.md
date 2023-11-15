## Got Tethics?

NOTE: This post contains spoilers for season six of the HBO television series *Silicon Valley*.

> In order to achieve greatness, we must first achieve goodness.  
> --Gavin Belson, Silicon Valley

In the [opening episode](https://www.vulture.com/2019/10/silicon-valley-season-6-premiere-recap-episode-1.html) of *Silicon Valley's* sixth season, Richard Hendricks [testifies](https://www.youtube.com/watch?v=lXyeZA54bko) in front of Congress regarding his company's decentralized internet, PiperNet. He promises that his company will not collect user data, unlike the other fictionalized versions of big tech companies present in the episode, only to discover later that user data collection is in fact happening on his network. Fast forward to [episode five](https://www.vulture.com/2019/11/silicon-valley-recap-season-6-episode-5-tethics.html) of the season. Gavin Belson, Richard's rival, has created a code of technical ethics, or "tethics", for the technical industry to follow in the wake of the congressional hearings. Richard is [frustrated](https://www.youtube.com/watch?v=n9cdGXa-uyM) at what he perceives to be a lack of genuineness on Gavin's part, with much disagreement from others. And soon Richard discovers that the statements in the Tethics code of conduct are [plagiarized](https://www.youtube.com/watch?v=4SI9GfFJDz0) from other companies' mission and vision statements.

In a [tweet](https://twitter.com/alistairkyte/status/1199044721001271297) from Alistair Kyte, we can see what Gavin Belson's Tethics Code of Conduct looks like:

![Tethics: A Code of Conduct](/assets/images/Tethics.jpg)  
(Image source [here](https://twitter.com/alistairkyte/status/1199044721001271297))

As I've watched through these episodes and read through this fictional code of conduct, it has me wondering: what would an actual code of ethics for software development look like? [Let's get tethical!](https://vimeo.com/111360699)

In 1997, the ACM/IEEE-CS joint task force on Software Engineering Ethics and Professional Practices (SEEPP) developed a software engineering code of ethics. The short version of their code of ethics is included below, but the full version can be viewed [here](https://www.computer.org/education/code-of-ethics) and [here](https://ethics.acm.org/code-of-ethics/software-engineering-code/).

> Software engineers shall commit themselves to making the analysis, specification, design, development, testing and maintenance of software a beneficial and respected profession. In accordance with their commitment to the health, safety and welfare of the public, software engineers shall adhere to the following Eight Principles:
>  
> 1. **Public**: Software engineers shall act consistently with the public interest.
>  
> 2. **Client and Employer**: Software engineers shall act in a manner that is in the best interests of their client and employer consistent with the public interest.
>  
> 3. **Product**: Software engineers shall ensure that their products and related modifications meet the highest professional standards possible.
>  
> 4. **Judgment**: Software engineers shall maintain integrity and independence in their professional judgment.
>  
> 5. **Management**: Software engineering managers and leaders shall subscribe to and promote an ethical approach to the management of software development and maintenance.
>  
> 6. **Profession**: Software engineers shall advance the integrity and reputation of the profession consistent with the public interest.
>  
> 7. **Colleagues**: Software engineers shall be fair to and supportive of their colleagues.
>  
> 8. **Self**: Software engineers shall participate in lifelong learning regarding the practice of their profession and shall promote an ethical approach to the practice of the profession.

It's a good list, and I would encourage you to look at the full version. I especially like the callout to management in this listing. As I have [previously](https://www.matthewyancer.com/2023/10/17/software-organization-anti-patterns.html) [covered](https://www.matthewyancer.com/2023/10/19/project-estimation.html#:~:text=whole%20host), there are a variety of questionable behaviors that management can bring to an organization that can impact the software development process. Good to keep these in check.

Another great set of ethical principles comes from Bob Martin's 2015 talk, [*Expecting Professionalism*](https://youtu.be/BSaAMQVq01E?t=677). I have included a listing and summary of his main points (with timestamps) below:

> - [**We Will Not Ship $#!+**](https://youtu.be/BSaAMQVq01E?t=1404): We will not knowingly ship code that is defective or substandard.
>  
> - [**We Will Always be Ready**](https://youtu.be/BSaAMQVq01E?t=1537): At the end of every development cycle, the code will be deployable.
>  
> - [**Stable Productivity**](https://youtu.be/BSaAMQVq01E?t=1725): You will produce features just as fast a year from now as you produce them today.
>  
> - [**Inexpensive Adaptability**](https://youtu.be/BSaAMQVq01E?t=1950): The business should not find it expensive to adapt the system to new requirements. It should be easy to change the code.
>  
> - [**Continuous Improvement**](https://youtu.be/BSaAMQVq01E?t=2018): The software gets better with time, the code gets cleaner with time, the designs improve with time. Every system should be getting better and better, not worse and worse.
>  
> - [**Fearless Competence**](https://youtu.be/BSaAMQVq01E?t=2103): If you had a comprehensive automated test suite that you trust, you could clean the code. If you could clean the code, then the code would always get better. If the code always got better, you could make it easy to change. If you could make it easy to change, you could go fast. That test suite is the key to everything.
>  
> - [**Extreme Quality**](https://youtu.be/BSaAMQVq01E?t=2496): Expect that the software is going to work release after release.
>  
> - [**We Will Not Dump on QA**](https://youtu.be/BSaAMQVq01E?t=2593): QA will find nothing.
>  
> - [**The Vast Majority of the Testing Will be Automated**](https://youtu.be/BSaAMQVq01E?t=2842): Manual testing always ends with you losing the tests. More commonly, you lose them by QA deciding not to run them. Because they don't have time. QA will decide which tests are the most important to run and which are the least important.
>  
> - [**Nothing Fragile**](https://youtu.be/BSaAMQVq01E?t=3165): Nothing in the system will be fragile.
>  
> - [**We Cover for Each Other**](https://youtu.be/BSaAMQVq01E?t=3185): If we're working in a team, if Bob gets sick, someone else should be able to step in and take over for what Bob was doing. And who's responsibility is it to make sure that someone can step in and make sure that they can take over for what Bob was doing? It is Bob's responsibility to make sure that someone can cover for him.
>  
> - [**Honest Estimates**](https://youtu.be/BSaAMQVq01E?t=3284): I want 3 numbers: the best case, the expected case, and the worst case.
>  
> - [**You to say "No"**](https://youtu.be/BSaAMQVq01E?t=3578): You were hired for your knowledge. And your knowledge gives you the privilege and the responsibility to say "no" when "no" is the answer.
>  
> - [**Continuous Agressive Learning**](https://youtu.be/BSaAMQVq01E?t=3752): You, as software developers, should be learning all the time. Learning a new language every year or two. You should learn new platforms, new operating systems, new frameworks. You should be fiddling around, playing with stuff. All the time. Because our industry is one that is constantly changing.
>  
> - [**Mentoring**](https://youtu.be/BSaAMQVq01E?t=4028): Half the programmers in the world have less than 5 years experience. Which puts our industry in a state of perpetual inexperience. How do we address the fact that all of the experience shrinks to insignificance in the face of the massive number of young graduates pouring out of the universities and getting hired. University does not prepare you for what's really going on in industry. It would be wise for companies and programmers to make sure that new kids coming out of school are not allowed to touch any of the core code for a year or so. Take them on as apprentices. Mentor. Teach. Make sure they're not turned loose on their own.

As I look through this list, it is clear that in order to meet these statements, you must change the way you tackle software projects. What planning you do up front, the technical approaches you use throughout the project, the underlying design of the system, and the roles that various personnel play at every step. It's not enough to just deliver the requirements here and now; it's necessary to consider impacts over time. It's worth some additional consideration.

I'm reminded of a previous customer of mine, whose stated goal was not to be merely compliant but to be above reproach in everything they did. What do you think are essential items to cover in a software development code of ethics?
