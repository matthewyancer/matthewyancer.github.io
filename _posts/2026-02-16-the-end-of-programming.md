## The End of Programming

I recently re-watched an [AI talk by Dr. Matt Welsh](https://www.youtube.com/watch?v=JhCl-GeT4jw) (former Harvard professor). Old in AI years. Ancient.

The talk’s core bet (as I hear it) is:

> LLMs will be able to produce any software system humans can.  
> And they’ll do it without “technical resources” being the constraint.

The details may already be out of date. But the thesis isn’t—because this isn’t really about GPT-4 versus GPT-5 versus whatever comes next. I’m using Welsh here as a stand-in for a belief I keep hearing:

That software would be easy…  
if it weren’t for the engineers.

That the job is “build the thing.”  
And everything else—estimates, reviews, architecture, testing, constraints—  
is friction.  
Excuses.  
Delay.

Wouldn’t it be great if we could just remove the need for the engineers altogether?

LLMs don’t create that belief. But they make it sound plausible.

*Let the AI write the code.*

And then Welsh goes even further: language models will eventually remove the need for code artifacts entirely. Wouldn’t that be amazing? (We’ll take that claim on in the next post in this series.)

Here’s the problem: LLMs make code cheap, which makes it tempting to treat engineers as overhead. But engineers are the mechanism that turns “working-looking output” into trustworthy software.

Demos are about output. Engineering is about consequences.

LLMs don’t remove the need for engineers.
They remove the illusion that typing was the job.
This post is about the illusion.

### The part he’s right about

Copilot-style tools are a real productivity jump. They keep you in the zone. They cut the “Google for syntax → get distracted → crawl back” tax. They turn a lot of daily programming into “nudge, accept, steer.”

The bigger point is the interface shift. Natural language is becoming a usable UI to computation. For a whole class of problems—summarization, classification, transformation, rewriting—natural language isn’t just a nicer interface. It *is* the program.

And cheap drafts change how people build. When iteration gets fast, you explore more branches. You try more ideas. You spend less time fighting syntax and more time steering toward intent. That’s real leverage, and it’s not going away.

He’s also right that a lot of what we call “programming” has always been trial and error. We act like we derive software from first principles, but most of us discover it by running it, poking it, and fixing what breaks. LLMs compress that loop.

But Welsh is most honest in the Q&A, when someone asks the question that matters: if the AI generates code a human can’t understand… how do you test it? His answer is basically: good question. Open question. We don’t really know yet. That’s not a footnote. That’s the center of the board.

### Code is cheap. Correctness is expensive.

A lot of AI hype measures software by the cost of producing code.

That’s understandable if you’ve never had to own a system after it ships.

Production software isn’t “code output.”

It’s behavior under edge cases.  
Performance under load.  
Security under hostile inputs.  
Observability when things go weird.  
Reliability when dependencies fail.  
Compliance when auditors show up.  
Response when the pager goes off.

A model can generate 20,000 lines of code in seconds.

Cool.

Now ship it.  
Secure it.  
Operate it.  
Evolve it.  
Prove it.

Typing was never the hard part.  
We just pretended it was because typing is what you can see.

And once you believe typing is the job, the math starts looking irresistible.

### The 12-cent developer

Welsh kindly does a cost comparison for us.

He assumes (roughly) a fully-loaded engineer costs about $1,200/day, and produces ~100 lines of code per day. Call it ~10 tokens per line. At the time, he uses a price around $0.02 per 1,000 tokens.

Do the math and you get the punchline:

Pennies.

He lands on “twelve cents”, but the slide doesn’t show the full arithmetic. That’s fine—the exact figure doesn’t matter—and LOC/day is a bad metric anyway.

The move he’s making is what matters:

Treat code output as the product.

This is persuasive theater. And it’s a category error. He compares **subsidized marginal token prices** to **fully-loaded labor costs of shipped software** and pretends that’s an apples-to-apples unit conversion. Maybe this is how they do math at Harvard. When I was in school, we were taught to pay attention to units.

A token price isn’t the total cost of “getting software.”  
It’s the price of one draft. At one point in time. Subsidized by a pile of capex, energy, and a business model that may or may not survive.

And it ignores the multiplier that actually matters:

How many iterations until it’s correct?  
How many until it’s safe?  
How many until it’s shippable?

That’s where the bill shows up.

### “Just regenerate it” meets reality

Welsh floats a liberating idea: if the model can generate the code and humans don’t need to maintain it, who cares if it’s messy?

If it breaks, blow it away. Regenerate it. Five seconds later you have a new version.

That sounds great right up until you ask: *who has to converge on this thing?*

#### The tester

If every draft is a brand-new codebase, QA doesn’t get faster.

QA resets.

There’s no “what changed?” because *everything* changed. No meaningful diffs. No bisecting. No confidence that accumulates over time. You just rerun the whole suite and pray you happened to cover the input you’ll see in production.

Generated code doesn’t remove the testing problem.

It amplifies it.

#### The product manager

Now apply the same dynamic to the product surface.

If every iteration can regenerate the UI, copy, and flows, you don’t “move faster.” You relitigate decisions you already made. The model will happily produce endless plausible variations. That’s great for brainstorming. It’s poison for convergence.

Product work isn’t “generate.”

Product work is “decide… and then hold the line.”

Consistency is a feature. Convergence requires memory.

And the moment your system is allowed to drift between iterations, you’ve traded engineering time for stakeholder fatigue.

#### The architect

And it’s not just a convergence problem. It’s a structure problem.

Good design isn’t just for humans. It’s for the machine, too. A ball of mud is expensive no matter who typed it.

The “humans won’t need to understand the code” line is puzzling for another reason. People were reading and writing machine language before JavaScript kids were born.

Unreadable isn’t new.

Unowned is.

Someone still has to care about the shape of the system: where the guardrails are, which invariants are enforced, what’s allowed to happen in what order.

If nobody owns that, you don’t get “AI-built software.”

You get an endlessly regenerating demo with occasional lucky green checkmarks.

To be clear: most teams aren’t actually blowing away repos every iteration. Today’s tools mostly do incremental edits—because diffs, stability, and rollback still matter.

But the promise being sold is still disposability. And even when you only regenerate parts of the system, you still have to converge on behavior you can trust.

### The thing the hype quietly assumes: a correctness oracle

At this point someone will propose the obvious fix:

Let the model generate the system.  
Then have another model test it.

Generate with a model.  
Review with a model.  
Test with a model.  
Iterate until it looks good.

This can absolutely help. It can catch obvious mistakes. It can raise your hit rate.

But it doesn’t create an oracle.

By “oracle” I mean a reliable way to decide—independent of the model—whether the behavior actually matches the intent.

Here’s the premise hiding under “no technical resources needed”:

Given an arbitrary prompt…  
the system converges on the desired correct output.

The moment you claim this loop can *guarantee* correctness for *arbitrary* requirements, you’re bumping into the same wall that shows up everywhere in computation:

There is no “button” you can press that reliably answers “does this program do what I meant?” for every program and every set of requirements.

Turing’s halting result is the simplest illustration. If you could universally and correctly decide key properties of arbitrary programs, you could decide halting too. You can’t. Not in general.

That doesn’t mean verification is hopeless. It means the dream of a universal “spec satisfied” button is fantasy.

Real engineering lives in constrained domains:

Tests.  
Contracts.  
Types.  
Staged rollout.  
Monitoring.  
Rollback.  
Living with uncertainty.

So when someone says “you won’t need technical resources,” what they often mean is:

The generator is cheap.

But cheap generation buys you drafts.  
Not correctness.

And drafts aren’t shipping.

### The intern metaphor, taken seriously

If you admit the output is “drafts,” the question becomes: drafts from *what*?

A tool?  
A compiler?  
A teammate?

Welsh’s best move in the talk is when he stops talking like it’s a machine and starts talking like it’s a person:

Treat the LLM like a very smart intern.

You don’t get guarantees.  
You get leverage.

You try it.  
You learn its quirks.  
You review its work.  
You decide what’s acceptable.

And yes—human society somehow still functions like that.

But if “intern” is the right metaphor, follow it all the way.

Interns don’t replace engineers.  
Interns are leverage *for* engineers.

Which means “no technical resources” isn’t the future.

It’s the marketing.

And if your plan is to encode your guardrails as tribal knowledge—“say do not in all caps”—then congratulations: you didn’t remove risk.

You automated it.

We already know what happens when your guarantees live in social interaction:

You ship inconsistency.

LLMs don’t fix that.  
They scale it.

### What changes (and what doesn’t)

If the model is an intern, the work doesn’t disappear.

It moves.

People will try to rename that work “supervision.”

Call it whatever you want. It’s still engineering.

You spend less time typing.  
More time specifying.  
More time verifying.  
More time building guardrails that don’t live in anyone’s head.

That’s the part the hype keeps skipping. It treats engineering as overhead because the output looks plausible.

But plausibility isn’t correctness.  
And correctness is the whole job.

LLMs don’t remove the need for engineers.  
They remove the illusion that typing was the job.

And the faster we can generate software-shaped drafts, the more we’re going to need people who can say:

“No. Not like that.”  
“Here’s the invariant.”  
“Here’s the test that matters.”  
“Here’s the blast radius.”  
“Here’s the rollback plan.”

---
A note to students (and parents): Computer Science was never about typing code. It is about computation:

What can be computed.  
What can’t.  
How efficiently.  
How reliably.  
Under what constraints.  
With what guarantees.  
In the presence of failure.  
In the presence of adversaries.

Because the easier it gets to generate plausible output, the more valuable it is to know where it breaks.

These principles are more relevant now than ever.
