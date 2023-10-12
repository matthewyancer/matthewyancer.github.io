## Percent Complete

In an [earlier post](https://www.matthewyancer.com/2023/10/02/the-ninety-ninety-rule.html), I touched on inaccurate task completion percentage reporting. Let's take a look at how completion percentages can be correctly calculated.

Let's say you have a work breakdown structure as follows:

| Task Name | Estimated Hours |
| ----------- | ----------- |
| Task 1 | 10 |
| Task 2 | 15 |
| Task 3 | 5 |
| Task 4 | 20 |
| Task 5 | 10 |
| &nbsp; | &nbsp; |
| Total: | 60 |

Using this estimate, planned progress can be calculated. Take each task's hours as a numerator and the total project hours as a denominator. This tells you what percentage each task will contribute to the overall completion of the project as it is finished. Based on the above sample (and rounding to the nearest percentage), we arrive at:

| Task Name | Estimated Hours | Planned % |
| ----------- | ----------- | ----------- |
| Task 1 | 10 | 17% |
| Task 2 | 15 | 25% |
| Task 3 | 5 | 8% |
| Task 4 | 20 | 33% |
| Task 5 | 10 | 17% |
| &nbsp; | &nbsp; | &nbsp; |
| Total: | 60 | 100% |

As you track progress through the project, each task can only contribute at most the planned percents displayed above towards the project's total completion percentage. Once Task 1 is 100% complete, the overall project will be 17% complete. Once Task 2 is complete, an additional 25% of the project will be complete, bringing the total project completion to: 17% + 25% = 42%. After Task 3 is complete, the project will be 17% + 25% + 8% = 50% complete. This is the **Progress Percent**. You earn additional *progress* on the project as each task is completed.

The second type of percentage that can be calculated is the **Effort Percent**. As the developer(s) work hours on the project, take the number of hours worked as the numerator and the total planned effort as the denominator. So if one developer works on the project for 3 days, you would take: (3 days * 8 hours per day) / 60 hours. This gives an Effort percent of 40%. Or, in other words, 40% of the planned hours for the entire project have been consumed.

It's important to not mix up the Progress percent and the Effort percent. Let's say two developers work together on Task 1 for a day and finish it. The Progress percent will be 17% according to the table. The Effort percent (rounded to the nearest percent) will be: (2 developers * 1 day * 8 hours per day) / 60 hours = 27%. Meaning that the Effort exceeded the Progress by: (27% - 17%) = 10%. And this means you're on track to exceed the total planned hours for the project unless you can shave off some hours from later tasks.

Now let's consider the following work breakdown:

| Task Name | Estimated Hours | Planned % |
| ----------- | ----------- | ----------- |
| Task 1 | 100 | 17% |
| Task 2 | 150 | 25% |
| Task 3 | 50 | 8% |
| Task 4 | 200 | 33% |
| Task 5 | 100 | 17% |
| &nbsp; | &nbsp; | &nbsp; |
| Total: | 600 | 100% |

When the tasks have a longer duration, an undesirable thing happens. Let's say I have two developers working steadily every day on the project. At the end of week 1, I've consumed 80 hours on the project: (2 developers * 5 days * 8 hours per day). Which means I have an Effort percent of 13%. What's my Progress percent? Well, Task 1 isn't complete, and no other tasks have been worked on, so my Progress percent is 0%. So, I send a lovely message to management explaining how [we've consumed 13% of the budgeted hours to achieve 0% progress](https://www.youtube.com/watch?v=BcSXr1uTsGg). "But we're early in the project", I promise my boss. "Nothing to worry about. All under control." The next week isn't quite as bad, as the developers wrap up Task 1, giving me 17% progress. But my Effort percent has gone up another 13%, bringing the total Effort to 26%. And week 3 looks utterly abysmal, staying at 17% progress, but now with a [total Effort percent of 39%](https://www.youtube.com/watch?v=LY5h55duFUc)! I can just imagine the email response to that: "What do you mean there was no progress this week!?"

*All or nothing on the task completion isn't looking so good.*

What I would recommend in this case is defining milestones within a task that earn you a certain amount of progress at the task level. I have two favorite types of milestones that I like to use: credit for starting a task and credit for being ready to test a task.

You'll notice that there is a considerable lag between when a task starts and being able to recognize progress at the end of the task. So, what you can do is give a small amount of credit for starting a task—let's say 10% or 20%. Let's go back to that first week of work above. The two developers start on Task 1, but don't finish it by the end of the week. They're 80 hours into a 100-hour task; it isn't fair to say that they're still at 0%. Giving them 20% progress just for starting the task would mean that you could report: 20% * 17% = 3% total project completion (rounding to the nearest percentage).

Now, let's say being ready to test a task means you have finished out another 40% of the task. In one of your status calls with the developers during week 1, they inform you that testing on Task 1 has begun. So, you give them 3% for starting Task 1. And then you give them: 40% * 17% = 7% (rounding to nearest percentage). For a total of 10% overall project completion. You report to management 10% Progress with 13% Effort. This looks much better. Week 2, the developers finish out Task 1 and start Task 2: 17% + (20% * 25%) = 22%. Reported as 22% Progress and 26% Effort. Still looking good. Week 3, the developers are testing Task 2: 17% + ((20% + 40%) * 25%) = 32%. Reported as 32% Progress and 39% Effort. Much better!

This post has described a simplified version of Earned Value Management; for more information look [here](https://en.wikipedia.org/wiki/Earned_value_management).
