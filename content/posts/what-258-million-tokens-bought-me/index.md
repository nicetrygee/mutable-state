---
title: "What 258 Million Tokens Bought Me"
date: 2026-10-02
draft: false
---

I pay £18 a month for Claude Pro and I was pretty confident I was wasting most of it because I rarely hit my usage limit, and let's be honest,a limit you never reach feels like money left on the table. So I planned an experiment: switch to the pay-as-you-go API for a month and compare the bill with the subscription. If you'd asked me to guess, I'd have said my usage was worth about £10 a month. It was actually worth £63. Doh! I was out by a factor of six

## The logs already knew
I didn't need the month to find that out because Claude Code keeps a log of every session on your machine, token counts included, and an open source tool called [ccusage](https://github.com/ryoppippi/ccusage) reads those logs and prices them at API rates. So, one command against data I already had answered the question I was about to spend hours designing an experiment around. I used Claude Code on 16 of the last 30 days, mostly Sonnet 5 and then Opus 5.5, and at Anthropic's published API rates that came to US$82.88. At 2 October's rate of £1 = US$1.3186 that's £62.85, three and a half times the subscription. Pro had paid for itself by 9 September, and that's before counting any of the extensive chat I do in the Claude app.

![Cumulative API-equivalent spend vs Claude Pro](api-vs-pro-cumulative.png)

## Every turn is a full replay
The total is less interesting than where it was spent. I'd assumed the cost of using a model was mostly the cost of what it writes, because output is the expensive token right? My output turned out to be 0.4% of my tokens and 17% of the bill. So, fresh input was effectively nothing. Of the 258 million tokens, 98% were cache reads, and they made up 61% of the cost, with writing to the cache another 22%.

That makes sense once you think about what an agent is doing. A model doesn't remember anything between turns. Every time a coding agent reads a file, runs a test or takes another step, the whole conversation goes back to the model: the instructions, the code it has read so far, and everything that has happened since. Caching makes each of those re-reads cheap, but an agent does it constantly and the volume adds up. Most of the cost of agentic coding is re-reading context. With a flat subscription, Anthropic sets the price expecting a typical subscriber to re-read a certain amount. If you re-read less than that, Anthropic comes out ahead. If you re-read more, I do. Last month you re-read far more, so you came out ahead.

## Habits that make the biggest difference
How could I have worked smarter you ask? The answer is to change the way I work so that I re-read less. That means:

 - Start fresh between tasks. Use /clear when you switch to something unrelated. Otherwise every turn of the new task re-reads the old one.
 - Compact or restart at natural breaks. Once a plan is settled, start a new session from the plan or spec rather than carrying the whole discussion forward. This fits how I already work with Spec Kit. 
 - Keep the fixed overhead small. CLAUDE.md, the system prompt and the tool definitions for every connected MCP server go out with every turn. Trim CLAUDE.md and turn off MCP servers you aren't using in that project.
 - Point it at the right files. "Fix the null check in parser.py" costs far less than "find the bug". Exploring the codebase fills the context with files it reads once and then re-reads on every later turn.
 - Keep noisy output out. Large test logs, stack traces and build output stay in the context once they're in. Ask for tail, grep or a summary instead.
 - Use subagents for exploration. A subagent reads in its own context and only sends back a summary, so the main session doesn't carry everything it read.
 - Match the model to the task. Cache reads on Opus cost more than on Sonnet. Use Opus for design and hard debugging and Sonnet for routine edits.
 - Don't leave a session idle mid-task. The cache expires after a period of inactivity. When you come back, the whole context is written to the cache again, which is part of your 22% on cache writes.

## Vendor lock-in, metered
That doesn't mean I'm getting £63 of compute for £18. The API rate is a list price with a margin in it, not what it costs Anthropic to serve me, and a subscription works like a gym membership: the people who barely use it pay for the people who do. What bothers me more is that the way I work is now built around a flat price I don't control. If the deal changes, and tighter usage limits are more likely than higher prices, I have no fallback.

Does this mean companies have the same problem at a bigger scale? A company that rolls out agentic coding on per-seat licences is budgeting for the subscription, not the usage. The real cost driver is how much context gets re-read, which depends on how each engineer works, and I wonder if FinOps tracks it. If you're responsible for AI adoption, I think measuring that should be part of the rollout, because the logs to do it are already sitting on everyone's machine.

## Same workload, cheaper backend?
That changes the question I want to answer. Pro isn't overpriced for the way I work, so another month comparing the same models on a different billing plan would teach me nothing. The more useful question is whether I can get the same performance from cheaper models, which would also give me the fallback I don't have. So for my next experiment I need to point OpenCode at models available through OpenRouter, give them the same kind of work, and see whether the quality holds when the context costs a fraction of the price.

The first lesson was cheaper than I expected: before designing an experiment, check whether you're already collecting the data that answers it. I was, and it took me one command to find out.
