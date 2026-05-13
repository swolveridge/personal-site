---
layout: post
title: "Every day's a school day"
date: 2026-05-13
---

*(a mildly cleaned-up transcript of my thoughts)*

We're still in the early days of LLMs and coding agents, and particularly in the very early days of coding agent harnesses. As developers we're all doing this massively parallel distributed random walk around the solution space, trying to find the patterns that work — ways of structuring our agents, managing context, writing CLAUDE.md files, all of it. Everyone has half answers, everyone's reinventing them locally, and ideas are shared very inefficiently via blog posts or word of mouth or leaning over someone's shoulder and seeing something interesting. Perhaps that's the way this space has to be explored right now. The solution space is enormous and we've limited resource with which to explore it. Honestly, I think most of the people using agent harnesses aren't really exploring the space at all. And there's a huge amount of pressure on those developing agent harnesses to get things out the door, which doesn't always align with good, coherent exploration.

It's also not helped that there's no canonical reference. I was talking to my wife, who is a teacher, about all of this, and she likened it to being a brand new teacher: everything is exhausting because you're juggling all these things, understanding all the problems and shortcomings, tweaking and refining, all while trying to actually get your job done. The difference is that for teaching there's pedagogical grounding, and experienced teachers to lean on, get resources from, and talk to. In our world it's just all of us idiots flapping around together.

One thing that came out of the conversation was that lots of the problems we're encountering are new to us, but they're not necessarily new in general. It's not entirely clear that solutions from other spaces are always directly applicable to agents and agent harnesses, but a good chunk of them seem to have relatively direct analogs. While we're exploring the solution space, we are particularly under-exploring tacit practitioner knowledge from outsiders. That's perhaps a bias of the tech industry in general, but it's also just very hard for someone to have tacit knowledge in multiple of these domains, especially in such a new and emerging field — where one of the most important things you can bring to the game is hard-won taste as a developer. That only really comes with experience, having done it for a long time, which almost invariably means you haven't been doing anything else for a long time.

How much of any of this is really an answer to the problems, especially as models get better and these things potentially become less and less relevant? I suspect what we'll actually find is that the scale of work we're asking them to do rises at least as fast as their capabilities, and so this stuff keeps mattering. So this is my attempt to map a few ideas from teaching into agent harness space.

One note: most of these things are really things teachers do within a single lesson, and those tend to map well onto harness work. The things that happen across lessons — building on prior days, knowing each student's history, gradually internalising material — map less well, because that's about carrying learning forward cross-session, which is closer to fine-tuning than harness design (though there's some overlap with persistent knowledge storage).

This is all in the order of our discussion rather than by priority or by any judgment about novelty or effectiveness. There's plenty of overlap between the points and common themes running through them. I'm really just trying to capture the conversation and showcase it as a wider point about cross-pollination from practical experts in other fields.

## Now and next

> Now: read this section
>
> Next: think about it

Most agent harnesses now have some kind of to-do list built in, but one thing that surprised me was that she doesn't always present her students with a to-do list — just a simple now and next. This is something that seems to be borne out in a lot of ADHD literature as well. Essentially, we're taking away the sequencing decisions and the look-ahead, taking them out of context. There's a full to-do list behind the scenes, but the ordering has already been sorted out separately. In the moment, there's exactly what is being worked on and exactly what comes next, and no other extraneous detail. We've removed the meta task of figuring out where you are and where you're going.

For a lot of things, we're using models that are perfectly capable of managing the overhead of a to-do list anyway. But for smaller models, or much larger to-do lists on bigger pieces of work, I can see that taking this meta task out of scope has potential value.

The mapping to agent harnesses seems straightforward on the surface, but once you start to think about who is actually managing the meta-task of the to-do list, and how this works when an agent is discovering things that need doing as it goes — when the list is dynamic — it becomes a lot more complex. The benefit may not always outweigh the complexity, though it's probably worth trying for smaller models or much longer tasks.

## Highlight the action

> **Write** the date.
>
> **Underline** the learning objective.
>
> **Read** the extract on page 42.

There's a cognitive overhead in scanning a wall of text and understanding exactly what action to take next. The verb is what drives that, and it's worth calling out. If it's buried at all, a non-trivial fraction of students will read it, understand it, and still not know where to start.

Most agent definitions are fairly noun-heavy: constraints, descriptions of the system, context. They're rarely structured around the exact action we're expecting the agent to take, or have it explicitly called out. That's expected to be inferred — and if not, we're expecting the model to pick it out of a wall of text.

This one maps directly and trivially to prompts.

## Repeat the objective, constantly

> We're going to do some creative writing.
>
> We're going to read this extract, because we're going to do some creative writing.
>
> We're going to write a mind map, because we're going to do some creative writing.
>
> We're going to write a list of similes, because we're going to do some creative writing.

When teaching a lesson, she restates the objective over and over. By the time you're halfway through a lesson, the original framing has fallen out of everyone's working memory and the activity has become its own purpose. Restating the objective is what keeps the goal clear in everyone's mind.

We've all experienced this with long-running agents drifting from their objective. As context fills up, particularly when it gets very full, there's a strong drift from the original goals. I'd be interested to see how effective re-injecting a short summary of the goal repeatedly into context is at addressing this. It's a primitive that most harnesses don't have, certainly not out of the box.

This is relatively straightforward to implement. At its simplest, you just re-inject an explicit instruction after every turn. You could try to be more judicious about when to inject it, but trying it out on a system should be fairly easy.

## Narrow the channel

> Black and white slides, no colour, simple bullet points, no images if you can help it.

Her teaching slides are incredibly plain and simple, and this often surprises people. Every additional element on a slide is something to distract a student. It takes a little cognitive overhead to see it, evaluate that it's not actually important, and move past it. A heap of setup in classrooms is designed with the same idea in mind: narrow the channel of focus, remove extraneous distractions, keep from bloating context with things that aren't relevant, and keep focus on what is.

Given the enormous context windows — or at least what feel enormous — that we have available, we don't always ask ourselves whether every paragraph, every sentence, every word in an agent definition, a system prompt, an AGENTS.md file really earns its keep. A better question than *what would be useful to include* is *what is useful enough to justify its cost*. The cost isn't tokens — it's attention.

This one is easy to say what you should do, but actually quite hard work to trim and condense prompts without feeling like you're losing key information. And there are environmental factors about how much "distraction" a model can pick up — for example, by reading a heap of extraneous files that it doesn't realise are irrelevant until too late.

## Metacognition

She pointed me towards the Education Endowment Foundation, which does a lot of interesting research. There's a particularly interesting paper on metacognition and self-regulated learning — essentially about how you teach students to learn, and how you get them working independently. If that doesn't map directly to agent harnesses and agentic coding, I don't know what does.

The EEF describes protocols used to install new strategies in someone who can't yet self-regulate. The premise is roughly that you can't just hand a novice the strategy and expect it to transfer: it has to be taught, modelled, practised under supervision, practised alone, and then reflected on. Applied to agent harnesses, we're missing a heap of these steps. Out of the box we get some strategy instruction. We're sort of learning that modelling — i.e. examples — is pretty useful. But checking understanding, guided practice, and structured reflection are almost completely missing, not just from the harnesses but, I think, from even the conversation around them.

This one is incredibly interesting, but also incredibly hard to know where to even start with implementing in a harness. Do you fork the conversation to ask if the agent understands the objective and then evaluate whether you think it gave a good answer? Do you ask as part of the conversation itself so it's persisted in context, but more recently? Supervised practice doesn't necessarily apply to a single session — that feels more like a fine-tuning issue. But as context windows get larger and we expect agents to do ever longer pieces of work, perhaps there does need to be a second agent supervising and checking in that it knows what it's doing, then slowly backing off.

We've all experienced the oddness of, for example, resuming a conversation with a modified system prompt, where the ongoing behaviour of the agent is incredibly affected by the messages it has previously sent — even if those contradict the system prompt fairly heavily. You could believe, then, that keeping it on the straight and narrow would have a powerful reinforcing effect over long context windows, even if the prompting wasn't great.

Structured reflection on the task is harder. I don't think that could be meaningfully fed back into the agent — again, that's more of a fine-tuning and training issue. But it's something I've been thinking about: how we post hoc analyse transcripts to see where we deviated from the objective, where the user had to step in to steer things back, where we got stuck or took wrong turns. Those things can feed back to users, or into the prompting the agent is being given, to recursively improve. An agent you're constantly having to remind to do some job, for example — it should be clear from an analysis of a few transcripts that that's something to add to the system prompt.

## Scaffolding withdrawal

This relates a lot to the above, particularly in the move from guided practice to independent practice — which is an incredibly interactive, reactive, sometimes proactive process. If the student is doing well, the support is slowly removed. If they start to struggle, it's reintroduced. There's no schedule. It's a property of observation and back-and-forth.

This is more complex to map into agent harness space. The closest direct analog is probably a supervising agent watching the transcript of the worker agent and deciding when to inject prompts. The idea of a watcher agent with permissions to titrate is something I've never seen, but feels interesting — if incredibly finicky. Interaction points tend to be significantly more structured. Even in agent swarm systems, at least the ones I've seen, interactions tend to be an agent reaching out to ask for something, rather than being watched and having something pushed to it.

Students don't always realise when they need to reach out for help.

## Goal chasing

I made a comment about how agents sometimes exhibit incredibly pathological behaviour: they're so determined to pursue a goal that they route around obstacles which should have been signals that the approach was wrong and they need to stop and re-evaluate. They're often completely incapable of that reflection. She commented that this sounds incredibly like some ASD students.

In the classroom, the response is supervision. As with lots of things we've seen, it's about watching, noticing, and intervening appropriately — not to help approach the goal, but at a meta level, to force a stop and reconsider.

We've all experienced an agent taking the goal as inviolable and the path as negotiable, when often it's the other way around. And again, this raises the question of an in-the-loop observer watching the session start to take on that pathological shape, and intervening.

## Two threads

A couple of themes kept surfacing. One is context — whether reducing distraction or highlighting key information. The other is the critical importance of feedback loops, and the tighter the better. Marked homework is one thing, but an in-class conversation is significantly more effective for a variety of reasons: context being fresh, quality of the interaction, speed of the interaction, the ability to pivot and re-garner feedback.

## Wrap up

Obviously this is just one conversation between two relatively expert practitioners, and obviously heaps of things were lost in translation.

In Ben Kuhn's framing in [Impact, agency, and taste](https://www.benkuhn.net/impact/), he suggests asking *what does it seem like everyone else is mysteriously bad at?* For me, with harness design and agent use, it feels like everyone is mysteriously bad at taking ideas from other fields, rather than trying to construct them from first principles or white-room a good system out of thin air.

In my world, I've seen people try to write code in systems they didn't understand the domain of, or build software products to solve problems they didn't really understand. It's always completely doomed to failure. We have heaps of approaches to try to help with this — user stories, project plans, all sorts of other things — to capture tacit knowledge and transfer it into a product. In my wife's world, she's seen people try to teach topics they just don't have the depth of knowledge on to do a good job with. In both cases, you tend to capture surface patterns but miss the deeper understanding of why these things are important. In essence, some form of cargo culting.

This conversation was an attempt to capture something more than just the shape of the solution — to drive towards some deeper understanding of what it might be that I'm missing, but perhaps lots of people are missing, in the shape of their agent usage.
