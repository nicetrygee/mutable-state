---
title: "I Was Out by a Factor of Six"
date: 2026-10-02
draft: true
---

I pay £18 a month for Claude Pro and I was sure I was wasting most of it. I rarely hit my usage limit, and a limit you never reach looks a lot like money left on the table. So I planned an experiment: switch to the pay-as-you-go API for a month and compare the bill with the subscription. If you'd asked me to guess, I'd have said my usage was worth about £10 a month. It was worth about £63!

I didn't need the month to find that out. Claude Code keeps a log of every session on your machine, token counts included, and an open source tool called [ccusage](https://github.com/ryoppippi/ccusage) reads those logs and prices them at API rates. One command against data I already had answered the question I was about to spend hours designing an experiment around. I used Claude Code on 16 of the last 30 days, mostly Sonnet 5 and then Opus 5.5, and at Anthropic's published API rates that came to US$82.88. At 2 October's rate of £1 = US$1.3186 that's £62.85, three and a half times the subscription. Pro had paid for itself by 9 September, and that's before counting any of the chat I do in the Claude app.

![Cumulative API-equivalent spend vs Claude Pro](api-vs-pro-cumulative.png)

The total is less interesting than where it went. I'd assumed the cost of using a model was mostly the cost of what it writes, because output is the expensive token. Output turned out to be 0.4% of my tokens and 17% of the bill. Fresh input was effectively nothing. Of the 258 million tokens, 98% were cache reads, and they made up 61% of the cost, with writing to the cache another 22%.

That makes sense once you think about what an agent is doing. A model doesn't remember anything between turns. Every time a coding agent reads a file, runs a test or takes another step, the whole conversation goes back to the model: the instructions, the code it has read so far, and everything that has happened since. Caching makes each of those re-reads cheap, but an agent does it constantly and the volume adds up. The work I think of as Claude writing code is mostly Claude re-reading context to decide what to write next. So the price of agentic coding is really the price of context, and a flat subscription is a bet that you'll re-read less than the provider expects. Last month I didn't.

That changes the question I want to answer. Pro isn't overpriced for the way I work, so another month comparing the same models on a different billing plan would teach me nothing. The more useful question is whether I can get the same performance from cheaper models. Next I'm going to point OpenCode at models available through OpenRouter, give them the same kind of work, and see whether the quality holds when the context costs a fraction of the price.

The first lesson was cheaper than I expected. Before designing an experiment, check whether you're already collecting the data that answers it. I was, and it took one command to find out.
