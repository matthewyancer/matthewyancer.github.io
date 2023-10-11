## Project Management Triangle

Early in my software development career, a project manager introduced me to the Project Management Triangle:

![Project Management Triangle](/assets/images/project-triangle.svg)  
(Image from [Wikipedia](https://en.wikipedia.org/wiki/Project_management_triangle))

There are three variables present in every project:

- **Time**, also known as project dates or project schedule
- **Scope**, also known as features or requirements
- **Cost**, also known as budget or resources

Changing one of these variables impacts the other variables on the project. Let's say you have a fixed number of resources assigned to the project, and there has been a specific set of requirements determined. Taking in both of these inputs, you could calculate a project schedule that allows you to deliver that set of features with this set of resources. You bring the projected schedule to management and learn that there is a critical deadline that has been promised that is exactly one half of the timeline you proposed. How do you meet this constraint? Well, there are two options: you can either cut the feature list in half or double the number of resources.

Likewise, if you double the requirements, a corresponding change would have to be made to either the resourcing or the timeline to successfully deliver. And if you halve the resources, you will have to halve the requirements or double the timeline. Cost, scope, time—you can pick two. The one you don't pick has to scale in response to the other two. It feels very mathematical.

*If only things were that simple.*

Very rarely are you given permission to scale one of the variables. You have a fixed team of resources, you have an inflexible set of requirements, and you have a dictated aggressive date. All predetermined. And to further complicate matters, very often resources are interrupted or pulled into other high-priority activities, additional requirements are added, and the date is pulled in. What do you do?

You could borrow resources from somewhere else. If the resource is idle or underutilized, this can be effective. But watch out. Use the resource for too long, and you may start to impact their other projects. You could also juggle resources around so that your project gets access to a more productive, more knowledgeable, and more skilled resource while still having the same overarching headcount. This "super" resource may be able to have a higher work output, allowing you to get more done in a shorter amount of time. But these types of resources tend to be [very rare](https://www.matthewyancer.com/2023/10/06/from-novice-to-expert-part-2.html) and it may be difficult or impossible to get access to them.

You could work salaried resources extra. Long days, nights, and weekends. Which works, but only for very short durations. Overwork a resource for too long without recovery, and the number of mistakes increases. You also risk resource burnout and the possibility of resignation. These mistakes have to be dealt with at some point, often at the end of the project. If this gets out of control, you will have serious issues on your hands. You could miss your deadline while fixing the mistakes. Or your project scope may not be met since non-working features are essentially missing features. And continuing to use a resource that was supposed to be freed up for another project is a cost overrun. You're putting all project variables at risk.

Keep in mind that not everything is in your control. Let's say the resources look at the aggressive date and seeing all of the extra hours of work ahead of them, decide to just code "quick and dirty". Take shortcuts. Slide on standards. Less care in the craftsmanship of the code. Less thought to design. Your project will appear to be in good health, meeting deadlines while resources are working normal hours, but good luck extending and maintaining the system. The project is building a steady stream of technical debt. Eventually, this will have consequences. It could hit on this project, adding unexpected efforts to the end of the project. Or it could hide under the rug, waiting to sabotage a downstream project.

Increased mistakes and technical debt touch on the fourth dimension of the project management triangle: **quality**. If you overly constrain cost, scope, and time, then you are likely to experience a decrease in quality. So what are some healthy options that can be used to deal with cost, scope, and time constraints without impacting quality?

One option I recommend is a **staged rollout**. Set up a plan for building all features in the project scope, but plan to release them in chunks. Focus on critical items and items needed for a minimally viable product in the early stages of the project. And plan for less critical and nice-to-have items in later stages. You will still "miss" your constraint date in that the entire project isn't finished, but hopefully you have enough of the important items ready prior to the constraint date to have effectively "met" the constraint.

Another factor to consider is team morale and **energy**. Software developers are knowledge workers. When they are happy and full of energy, tasks are easier and quicker to do. If the team is distraught and has low energy, tasks will take much longer. How do you increase energy? Take a look at the [Gallup Q12](https://www.gallup.com/q12/) for inspiration. Make sure you have measures in place so that your employees are likely to give favorable responses to these items.
