## The Ninety-Ninety Rule

As a follow-up to my [earlier post covering software development laws](https://www.matthewyancer.com/2023/09/30/the-first-law-of-computer-science.html), let's take a look at Tom Cargill's *Ninety-Ninety Rule*:

> The first 90 percent of the code accounts for the first 90 percent of the development time. The remaining 10 percent of the code accounts for the other 90 percent of the development time.

Or another phrasing I really like, from Juval Lowy:

> 90 percent of the time, developers are 90 percent done.

Early in my career, when I was a bright, up-and-coming full-stack engineer, I saw a perfect example of the Ninety-Ninety Rule firsthand. I was on a project with two developer peers. We were all cooperating, working on our separate tasks, with no developer lead in charge. Multiple times per week, we would have a call with a remote project manager. She would pull up the project plan and walk through our tasks, asking each of us what percentage complete we were. I started to notice quickly that one of my peers was giving wildly untrue percentages. The first day was 30%. Then 50%. Then 70%. Each meeting, the project manager was more and more pleased: *"Great work; maybe you can help these other guys speed up their tasks too!"* On the next call, the developer reported 90% completion. The project manager was ecstactic: *"Wow, you keep this up, and we're going to finish the project way ahead of schedule!"*

*Clue #1: Developers are rarely, dare I say never, ahead of schedule.* [See Parkinson's Law](http://wiki.doing-projects.org/index.php/Parkinson%27s_Law_in_Project_Management).

These status updates were bewildering to me. I had been watching this developer code every day. On the first day, barely anything had been done. Staring at the computer screen all day. An occasional mouse click. Is he writing it in his head, I wondered, planning out all of the keystrokes that would be played back later as a series of choreographed dance moves? The next day, I saw him crack open the requirements document a couple times. There were some lengthy discussions between this developer and another developer on the best approach for the sign-on process and logging. A little bit of typing here and there. But with each day, barely any evidence of progress.

Then the next meeting came. The project manager asked us where we were as always, and an impossible answer came back:

Developer: *"90%."*  
Project Manager: *"That can't be right; you were at 90% in the last call. Did you not get to work on this since our last meeting?"*  
Developer: *"Oh no, I've been working very hard. I found some items we had missed in task planning and worked on them. So now it's at 90%."*  
Project Manager: *"...I see, ok. But we're really at 90% now, right?"*  
Developer: *"Oh yes, 90% now."*  
Project Manager: *"Ok, good. Let's close out this last 10%. We're so close!"*

And then the next meeting:

Project Manager: *"Ok, where are we at today?"*  
Developer: *"91%."*  
Project Manager: *"91%?"*  
Developer: *"Yes."*  
Project Manager: *"That's with a whole day's worth of work?"*  
Developer: *"Yes."*  
Project Manager: *"Well, how can this be? I don't understand. We've been making such good progress up until now. Did you find some missing items again?"*  
Developer: *"Oh no, nothing like that. I hit some unexpected issues. But they're resolved now. Should be back on track tomorrow."*  
Project Manager: *"Ok, I understand. Let's get this closed out. Only 9% left to go."*

And the meeting after that:

Project Manager: *"Ok, are we making headway?"*  
Developer: *"Uh yeah, we're at 92%."*  
Project Manager: *"92%?! I don't understand. We were making such great progress before, and now we're only going up 1% each meeting!"*  
Developer: *"Well, I had to help other developer and I didn't get to put in as much time as I had hoped. But I might be able to make up some headway tonight..."*  
Project Manager: *"Other developer, is this true?"*  
Other Developer: *"Well, I did have a question, but it didn't take very long."*  
Project Manager: *"Developer, he's saying it didn't take very long. Why did this interrupt you?"*  
Developer: *"Well, yeah, our conversation wasn't too long, but I did have to do a bunch of research on it."*  
Project Manager: *"Ok, let's stay on task. You're so close! Let's get this done."*

And so it went. At each meeting, another 1% was added to the total. 93%. 94%. 95%. Then it remained stuck at 95% for multiple days. Followed by incremental counting again until 99% was reached. Then it stalled there.

The project manager was making periodic site visits now. Calling us all into the conference room to grill us on the project schedule. The casual days of staring at the computer screen, barely doing anything, were long gone. The developer was furiously typing every day. Coming in early, staying late. Working from home every night. Working through the weekend. I'm not sure that 100% was ever reached. The developer just moved on to the next task in the end.

My advice to software project managers:
1. **Avoid asking developers for percentages.** Most developers have no basis for how to actually determine their percentage and will make up a number.
2. **Be skeptical of early reports of fast progress.** This is more likely to indicate resources are not sure where they actually are on the task and may just be telling you what you want to hear.
3. Ensure that there are **verifiable gates throughout the project plan** so that you can establish a firm handle on what is actually done instead of using statuses based on feelings.
