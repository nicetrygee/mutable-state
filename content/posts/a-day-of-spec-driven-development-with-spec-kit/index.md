---
title: "A Day of Spec-Driven Development with Spec-Kit"
date: 2026-09-24
draft: false
---

Earlier this week I was at AI Camp's Sydney meetup about Forward Deployed Engineering. I was discussing spec-driven development with an engineer I met and he recommended that I check out Spec-Kit. This is GitHub's free, open-source toolkit for spec-driven development and it's reasonably mature....for an SDD framework. So I spent a day trying it out, and this post is about what I learned.

An AI coding agent has no memory worth relying on, so anything you want it to remember has to live somewhere it can read. That was the principle I took into my small experiment with Spec-Driven Development.

The setup was deliberately unambitious. I installed GitHub's Spec-Kit, drove Claude Code from Warp, and built a weather app for Australian places: search for a suburb, see the current conditions, behave sensibly when the network doesn't. I accept that nobody needs another weather app but I wanted to know what Spec-Kit feels like with tools I already use, and a small, boring product is a good way of keeping my attention on the process.

## The workflow, as it happened

Spec-Kit starts with a constitution, a set of project-wide principles that every later step is checked against. Mine has ten, each with a priority tier: privacy by design, trustworthy when things go wrong, accessible to everyone, simple over clever, tested before shipped and so on. It was already at version 1.3 by my first commit. The 1.3 change added the principle I'd recommend to anyone trying this: the agent must explain every non-obvious technical decision in plain language in the plan.

![The Core Principles section of the constitution, showing the priority tiers](core-principles.png "Ten principles, each with a tier. Explainability was added in version 1.3, before any code existed.")

From there the steps were **specify**, **clarify**, **plan**, **tasks** and **implement**. The first feature's spec ran to 24 functional requirements and seven measurable success criteria. The spec left one question open for me, whether the app should reopen on the last place viewed, and I chose to start on search with a "Last viewed" shortcut instead. Planning also did actual research, including live calls to the Open-Meteo API, and produced thirteen explained decisions covering things like why there's no navigation library and why the age of the data comes from the provider's timestamp rather than when the phone downloaded it.

Research also found something I hadn't considered. Shame on me. Open-Meteo is free for non-commercial use, which suits a free, ad-free app but stops suiting it the moment I add adverts. I read the terms, confirmed the interpretation and amended the constitution to 1.4, so attribution, caching and 'no ads' became binding rules in memory. More importantly, not my memory! This is the part of SDD I like most. A fact discovered once becomes a constraint that every later session is checked against.

![git show b4a8706: the constitution diff from 1.3.0 to 1.4.0 adding the Open-Meteo terms](constitution-v1-4-diff.png "A licence condition found during research, turned into a constitutional rule before any code was written.")

The Tasks step turned the feature into 58 items across six phases, with the failing test written before each piece of code and a commit at the end of every phase. The first user story was committed by lunchtime and then the afternoon covered offline fallback, unusual searches, an accessibility and security pass and a manual check on my iPhone, and the feature was merged the same day with 186 passing tests.

![The weather app running on an iPhone in Expo Go](iphone-screenshot.png "The finished feature on a real phone, where the spec finally met the outside world.")

## What worked

The documents did the job of memory. When I opened a new Claude session and typed 'let's pick up where we left off', the agent didn't need a recap. It read the checkboxes in tasks.md, saw the first user story was finished and started on the next task. Everything it needed for the second story, down to the exact wording of the error messages, was already written down.

![Handover summary in Warp: 32 of 58 tasks done, next up Phase 4](handover-checklist.png "The whole handover was a checklist in a markdown file.")

Tests-first held up as a contract. Each task named the test to write, with specific inputs and expected outputs, so 'done' was decided by the test suite. The agent wrote the test, ran it, wrote the code and ran the test again. It didn't have to guess what 'done' meant, and I didn't have to guess whether it had done it. 

The explainability principle is worth the investment because it means the plan reads like a design document a new joiner could follow, including the rejected alternatives and trade-offs for each decision. I could review the agent's reasoning before any of it had become code, which is a lot less stressful than reviewing it afterwards.

![Principle X, Explainability, in full](explainability-principle.png "Principle X in full, including what counts as a non-obvious decision.")

## What didn't work

I love docs but the documentation is heavy for something this size. The constitution and feature documents come to about 1,400 lines. The app is about 1,000 lines of code and 1,000 lines of tests. That's more writing about the thing than the thing. Most of it is decisions I'd otherwise carry in my head, so I don't think it was wasted, but the ratio would have to come down for SDD to pay its way on small changes.

The specs were also confidently wrong in places, and always about the outside world. The plan named a React Native version the Expo template doesn't ship. It didn't foresee that the app needed a library to keep content clear of the iPhone notch, so a new decision was added mid-build with a note admitting it. One task told the agent to expect version 3 of a storage library and not assume version 2; Expo installed 2.2.0. The manual test plan asked me to reopen the app in flight mode, which can't work in Expo Go because it loads the app over Wi-Fi from your local machine. The spec was consistent with itself but I guess it just hadn't met a real phone yet. Everyone has a plan until they get punched in the face. Mike Tyson said that, not me btw.

![Decision D13 in plan.md, marked as added during implementation](plan-decision-d13.png "The plan recording its own gap instead of quietly changing.")

## Three agents at once never grows old

For the third user story I ran three agents in parallel, each in its own Warp pane and git worktree. The split was easy because tasks.md already recorded which tasks touched which files. Each agent got one test-and-code pair, a list of files it could edit and two rules: don't touch tasks.md, and don't start the Expo dev server. All three committed within a minute of each other and the merge had no conflicts.

![Warp split into three panes, one Claude Code agent per worktree, each reporting its finished task pair](warp-three-agents.png "Three agents that never knew about each other, coordinated through one text file and three prompts.")

![git log --graph showing the three us3 branches merging into 001-place-search-weather](git-log-graph.png "Three branches, one merge, no conflicts.")

It was complete overkill. The whole story was only six small edits, and setting up worktrees, installing dependencies three times and writing three prompts cost about what running them sequentially would have. The biggest takeaway from this is the reason it was possible at all. The coordination was already in the documents before anyone thought about parallelism.

## Where I was still needed

My contributions were choosing the clarification option, reading a licence and deciding what it meant, deciding a dirty working tree should be thrown away, deciding whether parallel agents were worth trying, holding a phone with VoiceOver on and the text at its largest size, and choosing when to merge. None of that is writing code. All of it is judgement about the world outside the repository, or about risk.

## What changed

The interesting shift was where the conversation happened. Without SDD I talk to an agent about code and with SDD, I mostly talked to the agent about the md documents, and the documents told the agent about the code. They were the interface between us, between sessions and between agents.

That moves the human's job towards two things: writing constraints clearly enough that an agent can hold itself to them, and noticing when reality has drifted from what's written down. The agent was good at spotting drift. It flagged the version mismatches, the unworkable test step and the stray downgrade but it couldn't decide what any of them meant.

This was one small app, built by me in a day but it's really solidified my understanding of the constitution and the spec. They aren't paperwork for the agent. They're the part of the system I'm responsible for, which is familiar territory for an Engineering Manager / Technical Delivery Manager because most of the job is writing down what's been agreed and noticing when the world has moved on from it.
