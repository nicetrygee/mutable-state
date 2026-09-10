---
title: "Controls At Agent Speed"
slug: "left-of-the-diff"
date: 2026-08-31
draft: false
---

## The problem
An agent doesn't autocomplete a line and then wait for me. It's busy editing across files, running commands, and opening PR's while I'm still waiting for the kettle to boil. If code can arrive that quickly, and that unsupervised, I think my controls have to work at the same speed. Yes, code review is a backstop but it's not a primary control because it's late, it varies by reviewer, and volume overwhelms it very quickly. If the only thing standing between a plausible, but wrong implementation, and production is an (often) overworked human skimming a diff, that isn't a safety system that this old man wants to hang his hat on.

## I want my rules where matey agent can see them
Enter, md files. On a recent team we pushed the controls left, to the moment of generation, and made them travel with the code. In practice that meant documenting the standards and putting them where the agent will always read them, rather than hoping every engineer prompts well from memory. Concretely, that meant a markdown file the agent reads every run: an `AGENTS.md`, a `CLAUDE.md`, a rules file, whatever your tool happens to call it. It's onboarding documentation, except the new starter reading it is the model, every time and on every file. It covers conventions, commands, architecture, and the mistakes the team sees most often. Knowledge that used to sit in people's heads and on wikis becomes a file the agent reads at the start of every session, maintained by the whole team and iterated on whenever a mistake is made.

We did this in two layers. First, a repo-wide brief covering what's true everywhere. For example, the architecture, conventions, security baseline, and our non-negotiables.Then we added path-scoped files that attached the right rules to the right code, because the standard for our data-processing jobs wasn't the standard for our infrastructure module, and a single global rules file could either start contradicting itself or descend into much if one isn't careful. Scoping the guidance by where the code lives meant two engineers working in the same corner of the system tended to get the same shape out, without either of them having to remember the local rules.

## Why this shape and not alternatives? 
- A single global file can’t express ‘correct’ when correct differs by subsystem, and it grows into an unreadable catch-all. 
- Pure code-review governance also scales with reviewer time, which is exactly the bottleneck AI creates. 
- Baking rules into CI alone catches violations but doesn’t guide generation, so you get more failed builds, not better first drafts. - The layered, scoped approach means the AI’s first output is already close to compliant in the specific context it’s working in - which is what actually protects quality at volume.


## Gift wrap fiddly jobs in their own agents
For repetitive work that's easy to get subtly wrong, we went a step further and wrapped the whole task in a specialised agent with a deliberately narrow set of tools. We were onboarding data sources, where each new source touched config across environments and had to wire up validation and dead-letter handling identically every time, or you got drift that surfaced later in testing. An agent scoped to exactly that job, that refused to start without its inputs and baked in the safe defaults, turned a fiddly task or runbook into something quite boring. As an Engineering Manager, I never grow old of the boring things that have a tendancy to be the most reliable and scalable. 

## Caution: Guidance isn't enforcement
To be clear though: a markdown file is guidance, NOT enforcement. The model can ignore it, and sometimes will. The brief is there to shape the common case, but not to catch the bad one. Catching the bad one is the job of something deterministic that runs regardless of what the agent did, such as a CI, a linter, a policy check, or the review itself. The markdown improves your odds but the pipeline is what actually stops the exception reaching prod.

The remaining guardrails are cheap and well known, but I'll still state them anyway. We kept our secrets out of the context the agent can see, so there's nothing to leak. Made the test suite incapable of reaching the network. Kept AI-assisted changes on their own worktrees, behind review. This kept accountability with the humans in that whoever merged owns the code. At least to begin with.

## Consistency is king
Speed is the obvious benefit but dare I say, the least interesting one. The real payoff is consistency because a newbie in their second week produces roughly what a senior would, in a subsystem neither of them wrote, because the knowledge lives in the repo rather than in whoever happens to be around that day. It makes the safe path also the easy path, and it means the less experienced team member leans on the tool without being a bad PR away from an embarrasing incident. Strip the AI off it and that's just old-fashioned engineering excellence though....make the right way the default way.