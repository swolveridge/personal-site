## Working title

**The LLM Revolution Doesn’t Just Speed Up Coding — It Shifts the Bottleneck and Erodes Continuity**

---

LLMs change what's scarce - the ability to produce median-or-above quality code.
However, they don't solve social problems, or organisational problems, and the acceleration they provide is likely to make them worse.

What remains scarce is verification, rationale capture, senior capability (eg. high-level architectural oversight etc)
(and the social / epistemic machinery that keep systems coherent over time)

Some of these are (at least partially) solvable by throwing more LLMs at the problem, but other are only harmed by that approach.

---

## 2. The bottleneck shift (the core framing)

### 2.1 Production becomes cheap

* Code/text output becomes abundant; iteration accelerates.

### 2.2 Assurance does not automatically scale

* Testing, review, integration reasoning, architecture judgement, threat modelling remain scarce.
* If output rises, assurance must rise at least as much (otherwise quality becomes unbounded).

### 2.3 The masking effect

* Clean PRs, tidy diffs, passing tests can coexist with system-level decay.
* You can maintain a surface impression of health while the system-level story rots.

---

I can think of at least 5 different "pillars of failure"
THey're not independent, they overlap and even perhaps reinforce each other.

### Velocity vs assurance

- Assurance must increase _at least as much_ as output for quality to remain - and output is increasing _a lot_
- Tools that make complexity tolerable do not make it healthy - IDEs didn't suddenly make bad codebases better, they just made them easier to work with
- You must design your _system_ around fallibility - which you were hopefully already doing, since humans are fallible, though in different axes than LLMs

### Local correctness vs global coherence

- Visibility is not comprehension, navigation is not understanding - LLMs help the former, they _may_ help the latter
- Accidental architectures scale faster than intentional ones - especially given that LLMs tend to be 'inspired' by your existing code, rather than your in-head idea of the architecture you _want_, they're looking at the architecture you _have_
- Local checks can stop correlating with global correctness - LLMs are great at local correctness, but bad at global coherence (since they don't have the context for it - in at least 2 sense) - are integration and end-to-end tests more important than ever? Boundaries certainly are.
- Implicit invariants and accidental complexity can proliferate if boundaries are not kept strict - boundaries between components, libraries, systems - has to be done at every level
- The danger is not chaos; it’s smooth, locally-correct changes that accelerates global incoherence.

### Correlated error and the illusion of consensus

- If the same model writes the spec, implements it, then reviews it - you get correlated error, not independent checking - you wouldn't accept a dev doing their own reviews, we need diversity of thought/blind spots, we have systems built around this for humans, it's true for LLMs too
    - Should you agree on a model to use a a team? Should you share prompts across a team? Is correlation at _that_ level bad too?
- LLMs make agreement cheap (and are rather tuned to prefer agreement), leading to convergence on shared but unexamined assumptions
    - How often have you disagreed with an LLM about an approach as you would with a colleague, my guess is almost never if ever

## Homogenisation and latent senior-capability decay

- A less-obvious failure mode here is no obvious bad choices, it simply that _great_ choices may never be explored
    - The solution space drifts towards "good enough" solutions
    - LLMs rarely push back and suggest a bit re-architecture
    - Liable to get stuck in local maxima
- Loss of friction can lead to decay in engineering ability
    - How do you learn the hard lessons in this system?
    - Only noticed during re-architecture or incidents
- Can also lead to organisational loss of continuity - less cross-engineer discussion (since were all chatting with our LLMS) means less 'hive-mind', less cross-pollination of ideas, less shared context, less lesson-learning from others
- This could be seen as a process failure - but it's a new process we'll need
    - When writing code was hard, it _naturally_ produced senior engineers over time
    - How do you replicate the lessons learned?
    - Like a rich kid who makes a mistake and just has to say "oops, fix it someone please" - do they really learn the lesson?
    - Prompt and workflow design _can_ force breadth - but you need to do this _intentionally_
        - ANd how do you even _check_ this is happening?!

### Rationale and traceability as first-call artefacts

- This is very much not a new problem, just an exacerbation of an existing one
    - Akin to embracing outsourcing to devs you can never interact with again
    - Decisions happen not even in conversation, or in a head, but within an agent context
- "Why does this code exist?" is often solved with `git blame` + asking that person
    - What if that person no longer exists? Because they were an ephemeral context in an agent.
- "if it matters, it goes somewhere durable"
    - this has always been important, but rarely critical. Now it is
    - ADRs, design notes, spec documents, etc
- Given that people are lazy and feckless, actually this could be an improvement
    - The default stance is a slide into ephemerality
    - You need to build capture in UP FRONT
    - Treat it as a first-class concern in your agentic workflows
    - Automate the boring parts that humans know they _should_ do, but rarely _do_ do
    - Also need to include retrieval into pipelines
    - Notably, this has the universal design property - it's designed to help agents, but it helps _everyone_

---

## TL;DR

### Rules of thumb

* **Assurance must scale with output.**
* **Rationale must be durable or it will be lost.**
* **Local correctness is not evidence of global coherence.**
* **Independence beats agreement.**
* **You must actively protect solution-space diversity.**

### ?

* **Separation of duties for models:** one model/agent generates; a different one critiques/tests; don’t let one “own” an artefact twice.
* **ADR triggers:** define when an ADR/design note is mandatory (new invariant, interface change, architectural shift, security boundary, performance trade-off).
* **Reasoning to capture:** trade-offs, alternatives considered, invariant preserved/created, rollback plan.
* **System-level drift reviews:** lightweight but regular reviews focused on architecture coherence and implicit invariants (not code style).
* **Alternative-generation requirements:** require "three materially different approaches + trade-offs" for high-leverage decisions.
* **Traceability hygiene:** link code changes to decision artefacts; make "why" queryable.
