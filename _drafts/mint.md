I've been thinking about the correct way to prompt LLMs for coding, for coding agents.

And at the most basic level, there's just writing a message in the system to say, hey, write more tests to try and steer the behavior as you go. And that's clearly a bit nonsense, and extremely ephemeral, and just doesn't do a particularly good or consistent job.
So we take a step back, and there's AGENTS.md or CLAUDE.md or custom modes in Roo code and things like this, where you try to distill a little bit about how you want it to behave and give it some, this is the things you should do. And that's more consistent, but particularly in the infancy, those things are needing to be iterated fairly fast. 

And those become system-level prompts that sort of translate down into user prompt behaviors and how the LLM responds.

But I think perhaps the correct answer is to take a further step back.

So as models get better and better, the way these Claude.md files and system prompts need to be phrased definitely starts to shift. And if we take a step back and instead try to produce a document that captures our intentions and our ideals and our principles, and then use that document to generate Claude.md files and system-level prompts.

Now, one obvious way to do that is sort of manually look at it and go and make sure the prompts look how you want.
Another is to, in fact, just use a model, probably X-high thinking on a flagship model to do this, to turn principles into instructions and have those instructions turned into behaviors. So basically taking one extra level back. And so the system-level prompts, i.e., Claude.md, etc., sort of become a cache. 
They can be generated off of these principles. And this gives us a good place.
Those principles really aren't going to change. They can be developed very slowly, but they're mostly fixed for years at a time.
And this gives us a way to have our system-level prompts move as models change or be adjusted as we use different models that need slightly different tweaking, but while keeping the underlying principles the same and having some document we can refer back to on that.

How do you share them?
How do you copy/adjust them?
How do you personalise them?
All without losing their essence.

I think this principles document should actually also be incredibly useful for onboarding new developers into our team, because it encodes not only what we think is good software and good practice, but also a bit of our hive mind that helps you understand our codebases and approach to problem-solving.
And I would really hope that we absolutely aren't encoding model-level workarounds in it. 
I would be very happy for model-level workarounds to exist in the compiler that turns principles into practices. I think that's a totally reasonable place for those workarounds to live, to push things in particular directions. And I'd even be happy for the compiler to have slightly different, quote-unquote, compilation prompts for different models if we think that's appropriate.

priniciples
context
quirks
proto-prompts

https://github.com/swolveridge/mint
