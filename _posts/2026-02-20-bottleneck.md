---
layout: post
title: "The bottleneck is shifting"
date: 2026-02-20
---

LLMs change what's scarce – the ability to produce median-or-above quality code.
However, they don't solve social problems, or organisational problems, and the acceleration they provide is likely to make them worse.

What remains scarce is verification, rationale capture, senior capability (e.g. high-level architectural oversight and judgement, integration reasoning, threat modelling)
(and the social / epistemic machinery that keep systems coherent over time).
Some of these are (at least partially) solvable by throwing more LLMs at the problem, but others are only harmed by that approach.

The bottleneck shifts.
The trick is in predicting where the next bottleneck will be,
and hopefully designing a system that ideally avoids/ameliorates it, but at least doesn't get irreversibly harmed by running into it.

And you need to build (at least some of) this up-front – for example you cannot solve rationale capture post-hoc; it's *too late* and the rationale is irretrievably lost.

Note that many of these problems either only surface in the medium to long term, or are self-masking (tidy diffs, passing tests, but system decay – surface impression of health while the system-level story rots).

Also note, almost none of these problems are new – humans suffer from all of them – but we understand the shortcomings and ameliorations in human-space for these things. We are about to shift the system drastically though, and the question is really: how will these existing failures impact our future systems and workflows?

Many of these bottlenecks are not technical at all; they are organisational and incentive-aligned failures that LLMs amplify.

Here are some non-independent, overlapping thoughts about bottlenecks:

### Velocity, assurance and local correctness vs global coherence (verification / coherence bottleneck)

* Assurance must increase *at least as much* as output for quality to remain – and output is increasing *a lot*.
* Tools that make complexity tolerable do not make it healthy – IDEs didn't suddenly make bad codebases better, they just made them easier to work with.
* You must design your *system* around fallibility – which you were hopefully already doing, since humans are fallible, though in different axes than LLMs.
* Visibility is not comprehension, navigation is not understanding – LLMs help the former, they *may* help the latter.
* Accidental architectures scale faster than intentional ones – especially given that LLMs tend to be 'inspired' by your existing code, rather than your in-head idea of the architecture you *want*; they're looking at the architecture you *have*.
* Local checks can stop correlating with global correctness – LLMs are great at local correctness, but not necessarily at global coherence (since they likely don't have the context for it and lack stable system-level memory) – are integration and end-to-end tests more important than ever? Boundaries certainly are.
* Implicit invariants and accidental complexity can proliferate if boundaries are not kept strict – boundaries between components, libraries, systems – this has to be done at every level.
* The danger is not chaos; it's smooth, locally-correct changes that accelerate global incoherence.
* LLMs *can* be used to improve this situation, but they must be built carefully and intentionally to do this:

  * I've not seen much evidence of this happening in practice so far.
  * Most agentic workflows optimise for *throughput*, not architectural invariants or rationale capture.

### Homogenisation, correlated error and the illusion of consensus (epistemic / solution-space bottleneck)

* If the same model writes the spec, implements it, then reviews it, you get correlated error, not independent checking – you wouldn't accept a dev doing their own reviews; we need diversity of thought/blind spots, and we have systems built around this for humans; it's true for LLMs too.

  * Should you agree on a model to use as a team? Should you share prompts across a team? Is correlation at *that* level bad too?
* LLMs make agreement cheap (and are rather tuned to prefer agreement), leading to convergence on shared but unexamined assumptions.

  * How often have you disagreed with an LLM about an approach as you would with a colleague? My guess is almost never, if ever.
* A less-obvious failure mode here is no obvious bad choices; it is simply that *great* choices may never be explored.

  * The solution space drifts towards "good enough" solutions.
  * LLMs rarely push back and suggest a bit of re-architecture.
  * Liable to get stuck in local maxima.

### Latent senior-capability decay and rationale loss (capability bottleneck)

* Does it become more difficult to learn the hard lessons in this system?

  * This may only be noticed during re-architecture or incidents.

* This can also lead to organisational loss of continuity – less cross-engineer discussion (since we're all chatting with our LLMs) means less 'hive-mind', less cross-pollination of ideas, less shared context, less lesson-learning from others.

* This could be seen as a process failure – but it's a new process we'll need.

  * How do you replicate the lessons learned? LLMs don't feel the pain of an overnight support alert.
  * Like a rich kid who makes a mistake and just has to say "oops, fix it someone please" – do they really learn the lesson?
  * Prompt and workflow design *can* force breadth – but you need to do this *intentionally*.

    * And how do you even *check* this is happening?!

* Rationale loss is very much not a new problem, just an exacerbation of an existing one.

  * Akin to embracing outsourcing to devs you can never interact with again.
  * Decisions happen not even in conversation, or in a head, but within an agent context.

* "Why does this code exist?" is often solved with `git blame` + asking that person.

  * What if that person no longer exists? Because they were an ephemeral context in an agent.

* "if it matters, it goes somewhere durable".

  * This has always been important, but rarely critical. Now it is.
  * ADRs, design notes, spec documents, etc.

* Given that people are lazy and feckless, actually this could be an improvement.

  * The default stance is a slide into ephemerality.
  * You need to build capture in UP FRONT.
  * Treat it as a first-class concern in your agentic workflows.
  * Automate the boring parts that humans know they *should* do, but rarely *do* do.
  * Also need to include retrieval into pipelines.
  * Notably, this has the universal design property – it's designed to help agents, but it helps *everyone*.


## TL;DR

If the predicted failure modes above are real, the design response is not more output, but explicit counter-structures.

### Rules of thumb

* **Assurance must scale with output.**
* **Rationale must be durable or it will be lost.**
* **Local correctness is not evidence of global coherence.**
* **Independence beats agreement.**
* **You must actively protect solution-space diversity.**

### Things to maybe actually do

* **Separation of duties for models:** one model/agent generates; a different one critiques/tests; don't let one "own" an artefact twice.
* **ADR triggers:** define when an ADR/design note is mandatory (new invariant, interface change, architectural shift, security boundary, performance trade-off).
* **Reasoning to capture:** trade-offs, alternatives considered, invariant preserved/created, rollback plan.
* **System-level drift reviews:** lightweight but regular reviews focused on architecture coherence and implicit invariants (not code style).
* **Alternative-generation requirements:** require "three materially different approaches + trade-offs" for high-leverage decisions.
* **Traceability hygiene:** link code changes to decision artefacts; make "why" queryable.
