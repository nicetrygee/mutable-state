---
title: "Tales from the Terminal"
slug: "tales-from-the-terminal"
photo: mythical-man-month.png
photoAlt: "A shrink-wrapped copy of The Mythical Man-Month by Frederick P. Brooks, Jr., on a wooden table"
date: 2026-10-31T00:00:00+11:00
draft: false
---

*Editor's note (Nov 2026):* This article was originally written following my reading of the 1975 first edition of The Mythical Man-Month. I've since revisited and revised my thinking after reading the 1995 20th anniversary edition, incorporating Brooks' later reflections and the additional essays. The article has been updated to reflect that broader perspective.


## if manual_mode: interrupted() else: lost()
I build all of my projects with coding agents now, and for a long time every way of working with them felt like choosing which way I'd rather be annoyed.

In manual mode, I'm in on every step. Great! Love it! But the continual interrupts whenever it needs a decision drive me bonkers. In auto mode it gets on with the work, fast and quiet. Great! But before long I've lost sight of what's going on and lost control of my own project. I also read about people leaving agents to build overnight. Sounds great, but am I not then going to be spending all of the following day either reviewing a 7000 line diff or a mountain of ~400 line PRs? I suspect the engineers who get value from overnight runs pick work where 'done' can be easily signed off with a green build and the diff review doesn't require them to pore over it in fine detail. So maybe dependency bumps, rolling out a lint rule, adding type annotations, or fixing flaky tests. Or maybe work that produces something to read, instead of something to merge. Like a spike, or triaging a backlog.

## Switch faster, or review more?
Two claims doing the rounds on Reddit offer an explanation into the mindset of some people. First, 'engineering excellence has moved from flow to context switching', and the other is 'the future of software engineering is code review'. Both accept the problem, rather than solving it and I don't want to do either of those things. I want to get into flow and stay there.

## A new recipe for flow state
Since, I wrote a blog post earlier in the year called [A Day of Spec-Driven Development with Spec-Kit]({{< relref "a-day-of-spec-driven-development-with-spec-kit" >}}), I've used Spec-Kit on nearly everything I've built, and I've found it to be an absolute game changer. 

First, I find SDD gives me a way to establish clear decision boundaries before implementation begins. It forces me to think through the key decisions at each stage, define constraints and resolve ambiguity before the agent starts working. The result is fewer interruptions, fewer clarification loops and much less context switching.

More importantly, I retain ownership of the decisions. When reviewing the agent's output, I'm validating it against an agreed set of requirements, constraints and architectural choices that I've already considered and approved. I'm not trying to reverse-engineer the agent's reasoning or reconstruct why it made particular decisions.

The interesting thing is that flow state hasn't disappeared; it's just moved upstream. I'm now spending more of my uninterrupted thinking time shaping the spec and making decisions, while the agent handles the implementation. I'm still doing the thinking; I'm just changing when and where it happens.


## It's only Waterfall if you do it poorly
At first glance, SDD reintroduces several Waterfall style practices that Agile deliberately moved away from. For example, big upfront specs, more formal documentation, and reduced developer discretion. I would argue that it only resembles Waterfall if it's poorly implemented.

Done right, SDD establishes direction and boundaries, and doesn't prescribe every implementation detail. Here's the feedback loop it creates:

 - Define the problem, constraints and architectural decisions.
 - Break the work into small, independently deliverable increments.
 - Implement one increment.
 - Validate against the spec.
 - Review what was learned and update the spec where necessary.
 - Move to the next increment.

SDD and Agile are complementary. SDD provides the clarity and decision ownership and Agile provides the iterative execution and adaptation. The objective isn't to eliminate developer involvement or lock down every implementation decision. It's to move avoidable decision-making upstream so that implementation can happen with fewer interruptions.

## The Mythical Man-Month
One of my favourite books of all time is Fred Brooks's 1975 masterpiece, [The Mythical Man-Month](https://en.wikipedia.org/wiki/The_Mythical_Man-Month). Brooks was writing about the economics and psychology of software engineering decades before AI agents existed but several of his observations map remarkably well to the challenges of agentic development.

Brooks argues that great software needs conceptual integrity: a coherent design philosophy and a consistent set of ideas underpinning the system. This is particularly relevant to AI-assisted development because an agent can produce technically competent code while making decisions that are individually reasonable but collectively inconsistent. SDD provides a mechanism for establishing conceptual integrity before implementation.

## Optimise the size of the learning loop, not the size of the spec.
The most poignant insight from the book is that the first version of a system is often a learning exercise and you should expect to discover things that invalidate your initial assumptions. This is a useful counterbalance to SDD and there's a danger that teams interpret SDD as a requirement to get everything right before implementation but that's not the lesson I'd take from Brooks. The spec should be a living representation of current understanding, not a contract that prevents discovery. Brooks also advocates modularity, precise interfaces and controlled changes to make systems easier to evolve. These principles translate naturally into small PRs and bounded agent tasks. In other words, avoid enormous AI-generated PRs. They defer feedback, accumulate assumptions and make it harder to isolate mistakes.

## My recommendation for flow state with agents
Think before you build. Move cognitive effort upstream.
Constrain the work, not the creativity. Give agents autonomy within clearly defined boundaries.
Shorten the feedback loop. Small PRs, automated validation and continuous learning.
Protect the human's flow. Minimise interruptions, context switching and repetitive decision-making.

## Final thoughts
The central insight I'd take from Brooks is that software engineering has always been as much about managing complexity and preserving conceptual integrity as it has been about writing code. AI changes the economics of implementation but it doesn't remove the need for good engineering judgement. Flow state is about using that new implementation capacity without sacrificing the thinking, coherence and craftsmanship that make good software possible.