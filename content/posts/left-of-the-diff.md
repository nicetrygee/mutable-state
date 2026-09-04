---
title: "Controls At Agent Speed"
slug: "left-of-the-diff"
date: 2026-08-31
draft: false
---

An agent doesn't autocomplete a line and wait for you. It edits across files, runs commands, and opens the pull request while you're in a meeting. If code can arrive that quickly, and that unsupervised, your controls have to work at the same speed. Code review is a solid backstop but a poor primary control: it's late, it varies by reviewer, and volume overwhelms it before anything else. If the only thing standing between a plausible-but-wrong implementation and production is an often-overworked human skim-reading a diff, that isn't much of a safety system.

## Putting the rules where the agent can see them

On a recent team we pushed the controls left, to the moment of generation, and made them travel with the code. In practice that means writing the standards down and putting them where the agent will always read them, rather than hoping every engineer prompts well from memory. Concretely, it's a markdown file the agent reads on every run: an AGENTS.md, a CLAUDE.md, a rules file, whatever your tool happens to call it. Think of it as onboarding documentation, except the new starter reading it is the model, every time, on every file.

We did this in two layers. A repository-wide brief covers what's true everywhere: the architecture, the conventions, the security baseline, the non-negotiables.

### AGENTS.md
- Every new component ships with its tests.
- Never log request bodies; they can contain PII.
- Use the existing HttpClient wrapper, not raw fetch.

Then path-scoped files attach the right rules to the right code, because the standard for a data-processing job isn't the standard for an infrastructure module, and a single global rules file soon either contradicts itself or goes so vague it's useless.

### ingestion/AGENTS.md
- Every new source needs validation and a dead-letter queue.
- Apply config changes to all three environments, or none.

Scoping the guidance by where the code lives means two engineers working in the same corner of the system tend to get the same shape out, without either of them having to remember the local rules.

## Wrap the fiddly jobs in their own agent

For repetitive work that's easy to get subtly wrong, I'd go further and wrap the whole task in a specialised agent with a deliberately narrow set of tools. We were onboarding data sources, where each new source touched config across environments and had to wire up validation and dead-letter handling identically every time, or you got drift that surfaced later in testing. An agent scoped to exactly that job, that refuses to start without its inputs and bakes in the safe defaults, turns a fiddly checklist into something boring. Boring is the goal. I've come to think boring is the thing that scales.

## Caution: Guidance isn't enforcement

Worth being clear about one thing, though: a markdown file is guidance, not enforcement. The model can ignore it, and sometimes will. The brief is there to shape the common case, not to catch the bad one. Catching the bad one is the job of something deterministic that runs regardless of what the agent did: CI, a linter, a policy check, the review itself. The markdown improves your odds; the pipeline is what actually stops the exception reaching production.

The remaining guardrails are cheap and well known, but worth stating anyway. Keep secrets out of the context the agent can see at all, so there's nothing to leak. Make the test suite incapable of reaching the network. Keep AI-assisted changes on their own branches or worktrees, flagged, behind review. And keep accountability with people: whoever merges owns the code. At least to begin with.

## Consistency

None of this, to my mind, is really about speed. Speed is the obvious benefit and the least interesting one. The real payoff is consistency: a graduate in their second week produces roughly what a principal would, in a subsystem neither of them wrote, because the knowledge lives in the repository rather than in whoever happens to be around that day. It makes the safe path the easy path, and it means the junior can lean on the tool without being one bad afternoon away from an incident. Strip the AI off it and that's just old-fashioned engineering excellence: make the right way the default way, so the result doesn't depend on everyone being careful all of the time.