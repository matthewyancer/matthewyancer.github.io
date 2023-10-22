## Project Estimation

So, it's happened. Your boss comes to you asking for an estimate. You may be able to relate to this:

![Comic: XKCD Estimating Time](https://imgs.xkcd.com/comics/estimating_time.png)  
(Image from [XKCD](https://xkcd.com/1658))

Computing laws aren't much help:

>**Parkinson's Law**:  
>Work expands so as to fill the time available for its completion.

*Which implies that your estimate should be as small as possible.*

>**Hofstadter's Law**:  
>It always takes longer than you expect, even when you take into account Hofstadter's Law.

*Which implies that your estimate can never be big enough.*

And to further complicate matters, there are a whole host of [management political games](https://web.archive.org/web/20080922190914/http://www.thomsettinternational.com/main/articles/hot/games.htm) around estimates:

- Doubling and Add Some
- Reverse Doubling Option
- The Price is Right/Guess the Number I'm Thinking Of
- Double Dummy Spit
- The X Plus Game
- Spanish Inquisition
- Low Bid/What Are They Prepared to Pay
- Gotcha/Playing the Pokies
- Smoke and Mirrors/Blinding with Science
- False Precision

So, [what do you do](https://www.youtube.com/watch?v=rpMx4YY1syM&t=14s)?

I recommend the following:

1. **Select a Development Lifecycle**: The development lifecycle you use will have an impact on the tasks and overall flow of your project schedule. This may be pre-determined for you based on organizational standards, or you may have the [opportunity to consider](https://www.matthewyancer.com/2023/10/16/development-lifecycle-variability.html) project constraints and the individuals that make up your team when making your selection. There are many options across predictive, incremental, iterative, hybrid, and tool-based styles, each with their own advantages and disadvantages.

2. **Create a Work Breakdown Structure**: Make a list of the tasks in your project. Make sure to include the phases in your chosen development lifecycle. Include all parts of development, not just writing the code. You'll need to account for integrating, testing, fixing, tuning, and deploying. There are some good ideas for software work breakdown structures in [this post](https://www.joelonsoftware.com/2000/03/29/painless-software-schedules/) by Joel Spolsky.

3. **Use T-Shirt Sizing**: Take each of the tasks in your work breakdown structure and assign a relative t-shirt size to it (S, M, L, XL). A Small is half the size of a Medium, a Medium is half the size of a Large, a Large is half the size of an Extra Large. If you label a task as a Medium, it should feel half as big as a task that you have labeled as a Large. Review all of your t-shirt sizes to make sure they all feel roughly right. If necessary, you can also do in-between sizes to help fine-tune your estimate: S/M, M/L, L/XL. Now go through the exercise of estimating the hours for one or two of these tasks in detail. If your tasks are similar to historical projects, you can also reference the actual hours spent on them. Once you have these detailed estimates in a couple areas, you can then use them to expand your estimates across all tasks using the t-shirt sizing ratios I've laid out. This will give you hours for each task, and a total effort for the project. You may think you are done, but I promise you, what your manager will really want to know is the resourcing and project schedule/dates.

4. **Identify Task Dependencies**: You need to figure out what order the tasks should be done in. Determine if there are items that cannot be built or tasks that cannot be performed unless an earlier item is done first. Sort your tasks based on this sequence. If you have a large number of tasks, it's helpful to group them into chunks, and you can use the chunks in place of the individual tasks.

5. **Identify the Critical Path**: Based on your task dependencies, look for a sequence of dependent steps that is the longest. (It may help to draw a picture.) This longest sequence of steps will impact the overall delivery time for your project. Make sure you are staffing this sequence first, and make sure you don't let it slow down as you go through the project. Assign resources to the critical path and calculate dates for when each milestone of the critical path will be complete using your hours estimate and the number of hours each resource can work per day.

6. **Parallel Task Scheduling**: The tasks that are not part of the critical path can be fit into your schedule in dependency order based on whenever you have resource availability. If you have two developers working on the critical path and there are two more developers available who can't help with the critical path, give them non-critical path tasks to do. Calculate dates for these parallel tasks. Keep in mind that these parallel tasks need to be finished at the same time or before the critical path. If you add them at the end of the project after the critical path is done, then you have extended your critical path and lengthened the project.

7. **Finishing Touches**: Lay out the schedule in sequential date order of the milestones. Make sure you have accounted for any planned time off or holidays that the resources have. Add some buffer to the schedule if you feel it's necessary.

Congratulations! You have a basic schedule. Check [here](https://www.matthewyancer.com/2023/10/10/project-management-triangle.html) for considerations on adjusting project schedule variables. And [here](https://www.matthewyancer.com/2023/10/12/percent-complete.html) for recommendations on project tracking.
