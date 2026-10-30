---
title: "Tales from the Terminal"
slug: "tales-from-the-terminal"
photo: mythical-man-month.png
photoAlt: "A shrink-wrapped copy of The Mythical Man-Month by Frederick P. Brooks, Jr., on a wooden table"
date: 2026-10-31
draft: false
---

## if manual_mode: interrupted() else: lost()
I build most of my side projects with coding agents now, and for a long time every way of working with them felt like choosing which way I'd rather be annoyed.

In manual mode, I'm in on every step. Great! Love it! But the continual interrupts whenever it needs a decision drive me bonkers. In auto mode it gets on with the work, fast and quiet. Great! But before long I've lost sight of what's going on and lost control of my own project. I also read about people leaving agents to build overnight. Sounds great, but I would spend all morning reviewing all the PRs. I suspect the engineers who do this well choose work a test suite can check, like dependency upgrades or migrations, so a green build in the morning means it's ready to merge without a line-by-line review. Perhaps I need to get better at writing test cases.

## Switch faster, or review more?
Two claims doing the rounds on Reddit offer an explanation. Engineering excellence has moved from flow to getting better at context switching, and the future of software engineering is code review. Don't they both just describe ways of living with the problem?

## Moving the thinking upstream
For most of this year I've used spec-driven development (SDD) on nearly everything I build. I write a specification first: what should the system do, the decisions behind it and how I'll know it's done.....then Claude builds against it.

Last month I wrote a post about why that spec has to record your decisions rather than the tool's ([A Day of Spec-Driven Development with Spec-Kit]({{< relref "a-day-of-spec-driven-development-with-spec-kit" >}})). I'm no SDD evangelist but I genuinely do believe it's the best compromise I've found, and for two reasons:

 - The spec lets me concentrate. I am able to think long and hard before the agent starts, so nothing interrupts me, and the agent has far fewer reasons to stop and ask.
 - I own the decisions. When I review the agent's work, I'm checking it against choices I made, which is much quicker than reconstructing why it did what it did.

For me, flow is alive and well and it's moved upstream into the spec.

## Waterfall with a fresh coat of paint
SDD does have a cost, and it has an old name: waterfall. Writing the spec first means two things:

 - I lose the builder's discovery. Halfway through writing code by hand, you notice the abstraction is wrong, or that two concepts are really one. That insight comes from wrestling with the code, but the agent is the one doing the wrestling now, not me.
 - I commit before I've learned anything. Decisions go into the spec when I know least about the problem.

One of my favourite books of all time is Fred Brooks's 1975 masterpiece, [The Mythical Man-Month](https://en.wikipedia.org/wiki/The_Mythical_Man-Month). In the book he pointed to chemical engineers, who don't take a process straight from the lab bench to a full-sized factory. They build a pilot plant first, to learn what the lab couldn't tell them. His advice for software was to plan to throw one away, because you will anyhow. However, we kinda skipped the pilot, because building everything twice was too expensive.

## Fred's pilot plant is affordable now
With an agent, the first build now costs me a couple of hours. So before I write a spec, I have the agent build a quick throwaway version from a rough description, and I learn from it in three ways.

First, I use it. Clicking through shows me where the workflow feels wrong before any of it reaches the spec. Then I read its defaults, because the pilot shows what the agent does when I haven't told it anything, including its structure, naming, data model and error handling. My spec then records where I disagree. Lastly, I look for wherever the code is messy or confused, and the problem is usually badly defined, and that's where I need to go and think about the spec.

Sure, I'm watching the struggle rather than living it, and as a result I learn less than I would if I was writing the code myself. Even so, I get a good share of the discovery back for a fraction of the cost, and because regenerating code is so cheap now, most decisions in the spec are easy to reverse. The bits still worth agonising over are those familiar stalwarts that cheap code can't undo, like a schema with live data in it.

## The pilot that never gets thrown away
Here's my confession: I find it very tempting never to throw the pilot away. It works! Rebuilding it from a spec often produces something that looks more or less the same, so it feels like ceremony.

When I'm disciplined, I remind myself what the second build is really for. The pilot's code reflects the agent's defaults, and code built from the spec reflects my decisions. If I keep the pilot and write the spec afterwards, the spec just records the choices the agent already made. That's auto mode again, with a write-up attached.

![Diagram of a loop: rough idea, throwaway pilot, learn from it (use it, read its defaults, spot the struggle), write the spec, rebuild from the spec, then on to the next feature. A dashed red branch from the pilot labelled 'the tempting shortcut' leads to 'Keep it', then to 'Auto mode, with a write-up attached'](pilot-then-spec.png "Build a pilot, learn from it, and maybe err keep it.")
{.small}

There's a reasonable middle path: keep the pilot, write the spec as a list of changes and have the agent refactor towards it. Everything I noticed and disagreed with gets fixed, but a list of changes only covers what I happened to spot. A full spec makes me think through every part of the system, including the parts I'd never have looked at.

So Brooks's advice is finally affordable, and I still find it hard to follow :) Chemical engineers have it easier if you ask me. Who's going to be tempted to run a city's water supply through the pilot plant!?!?