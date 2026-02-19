
One of the most useful tools I've had the pleasure of interacting with in recent times has been Robocop (or at least, an internal 'fork' of [this](https://github.com/Smaug123/robocop))

It started life (and continues to exist) as a bash script that does an incredible simple job:
Take your diff against your merge-base, plus the full contents of any touched files, and send it to an LLM with a [prompt](https://github.com/Smaug123/robocop/blob/3c49f530b0d99b5d2ea9592c661b838f6f9130f3/robocop-core/prompt.txt) asking for it to spot 'obvious' problems.

Ive always known I'm a feckless fool - and I write code in such a way as to defend against that. Stong type systems, property-based tests, embracing Grug, etc - but even _I'm_ shocked at how much it catches. And how many things it catches that _didn't_ get caught in a human review.

It also has the unexpected side-effect of boy scouting your codebase, by which I mean leaving things better than you found them. It regularly points out issues elsewhere in files that you've touched (recent example, a missed `.iIspose` call for a field) which become easy drive-by improvements.

It's hard to imagine how many bugs it has fixed / prevented in the few short months that it has existed.

It's become hard to imagine living without it, in fact so hard that I built my own tribute act, [blart](https://github.com/swolveridge/blart), to use on my own projects.
Partly an excercise in agentic coding, partly in learning Rust, partly in handling LLM tool calling, but mostly because I no longer trust myself to write code without it.

