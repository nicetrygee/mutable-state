 ---
title: "Checklists and Interlocks for AI Evals"
slug: "ai-evals-2-checklists-and-interlocks"
photo: [PHOTO.jpg]
photoAlt: "[Alt text for the header still]"
date: 2026-10-28
draft: true
---

Welcome to Part 2 in my AI Evals series! In Part 1, I added logging and replay to Runway, my Engineering Manager planner. So that every time its Quick Add feature called the LLM, the request and the response were BOTH saved. I could then replay those saved responses to test my code without calling the model. Now, that setup only works if I follow a few rules: every model call goes through the logging, every prompt change receives a new version number, and nothing calls a paid model unless I’ve chosen to. At the end of Part 1, those rules were written down in my plan and in AGENTS.md, the instructions file my coding agents read, but nothing in the code actually enforced them. Now we're going to adds checks to the code that do.

## Checklists and interlocks

Aviation has two ways of making sure the right thing happens. The first is the checklist. Its modern form came out of a crash: in October 1935 Boeing's Model 299 prototype stalled on take-off because the crew had left a control lock engaged, and the pilots who flew it afterwards wrote a short list of steps to check before every flight. [Link to a source for the Model 299 story.] The second is the interlock: a mechanism that makes the wrong thing impossible. Many aircraft won't let you raise the landing gear while their weight is still on the wheels, however hard you pull the handle.

Checklists rely on people reading them whereas Interlocks work whether anyone remembers or not. Both have their place, and the useful skill is knowing which one each rule needs. The same split applies to instructions for coding agents. Most of us write our rules into a file like AGENTS.md, which is essentially a checklist that the agent reads and follows. In this Phase I try to turn as many of Runway's checklist items as possible into interlocks.

## Phase 1a in five pull requests

The [Phase 1a spec](https://github.com/nicetrygee/runway/blob/main/docs/slices/slice-e1a-guard-rules.md) split the work into five pull requests, each in its own git worktree:

1. **The last flight gets a recorder.** Runway's weekly summary still called Anthropic directly, so it went untraced. It now goes through the same doorway as Quick Add and runs on the local model, which also took the only paid call out of everyday use. I removed the Anthropic library from the project until Phase 1b needs it back.
2. **A guard on paid calls.** Any call to a model that isn't running on my own machine is now blocked unless I set a lab flag (`RUNWAY_LAB=1`). The guard runs before anything is sent, and a blocked call is still recorded, so the logs show what was stopped and why.
3. **A logbook for prompts.** Each prompt and its output format are fingerprinted, and the fingerprints are committed in a lock file next to the prompt's version number. Change a prompt without bumping the version and a test fails, with a message saying exactly what to do: bump, re-lock, re-record.
4. **Rules with named checks.** A new section of AGENTS.md lists eight rules for AI features. Each one names the check that enforces it, or says *review only* when nothing automated can.
5. **Replay on every change.** GitHub Actions now replays the Quick Add recordings on every push and pull request. It needs no model and no secrets, and it fails only when a recording is missing or something crashes.

## The rules, and what enforces them

This table is the heart of the phase. It turns a list of good intentions into a map of which ones the system defends and which ones I do.

| Rule | Interlock or checklist? | Enforced by |
|---|---|---|
| Every AI call goes through one doorway | Interlock | Linting bans the model libraries everywhere except `llm.py` |
| Every AI call is traced, including blocked ones | Interlock | Tests on the doorway |
| A prompt change bumps its version and gets re-recorded | Interlock | The lock-file test, and replay in CI |
| Paid calls need the lab flag | Interlock | The guard |
| Lab data is made up | Checklist | Review only |
| Test cases are written by a separate agent session, and I approve the answers | Checklist | Review only |
| AI output is a proposal, and a human approves any write | Checklist | Review only, until Phase 3 adds tests |
| Replay never quietly calls the model | Interlock | Tests on the runner |

The full rules are in [AGENTS.md](https://github.com/nicetrygee/runway/blob/main/AGENTS.md).

One detail I'm pleased with: a test runs the linter against a file containing `import openai` and checks that it gets rejected. A banned import that's only banned in the config file is still a checklist. The test proves the interlock is connected.

![Diagram showing rules sorted into interlocks and checklists](checklists-and-interlocks.png "Interlocks defend themselves. Checklists rely on someone reading them.")

## Pulling the handle on purpose

You only know an interlock works once you've tried to get past it. So, after the five pull requests merged, I pushed two throwaway commits: one bumped Quick Add's prompt to version 2 without re-recording, and the next changed the prompt wording, still without re-recording. CI replay failed, named every case with a missing recording, and told me to re-record. [Link the failed CI run, and add anything that surprised you about the failure message.] Then I reverted both commits.

I also ran Quick Add live against the local model and then replayed with the model switched off, to check that Phase 1a hadn't changed anything the model sees. [Confirm: did the scores match the Phase 0 run?]

## Here's what I learned

- **Give every rule an owner, even if it's you.** Writing *review only* next to a rule felt like an admission at first. It turned out to be the most useful part of the table, because it shows exactly where my attention has to go in code review.
- **Make the failure message do the teaching.** When the prompt test fails, it lists the three commands to run. An agent that hits it fixes the problem in the next step instead of guessing.
- **Record the blocked calls too.** Every blocked call leaves a trace, so I can see when the guard fired and why, and a dashboard can show it later.
- **Keep CI honest about what it knows.** Replay can prove my code and scoring didn't change. It can't tell whether a score is good enough yet, so for now CI fails only on missing recordings. Score thresholds come later, once I have enough runs to set them sensibly.
- [Add one thing from your explain-back note: something you had to work out yourself while reviewing the PRs.]

## How much did it cost?

Building Phase 1a with Claude Code took one day and used $8.13 of API-equivalent usage, measured with [ccusage](https://github.com/ryoppippi/ccusage). Running it is still free.

| Measure | Value |
|---|---|
| Cost | $8.13 |
| Model | claude-opus-5-5 only |
| Total tokens | 20.4M |
| Cache reads | 20.0M |
| Cache writes | 273K |
| Output | 105K |
| Input (uncached) | 280 |

[Confirm: ccusage counts all Claude Code use on the machine that day. Should the spec-writing session be included? 16 October shows a further $5.75.]

## What's next

Phase 1b adds depth: a written guide for how answers are scored, a bigger set of test cases including the awkward ones, repeat runs so one lucky result doesn't mislead me, a first dashboard, and a first comparison between a paid model and the local one. That paid comparison is the first time the lab flag gets set on purpose, which is exactly what the guard is there for.

## Key takeaways

For every rule you give an agent, name the check that enforces it. Where you can, make it an interlock, so the rule holds whether anyone remembers it or not. Where you can't, write *review only*, so everyone knows that one is on you. In my experience this applies just as well to teams of people as to agents: the rules that last are the ones the system defends, and the rest deserve to be listed honestly as someone's job.

*The code, spec and rules are in the [Runway repo](https://github.com/nicetrygee/runway), and Phase 1a is tagged [eval-phase-1a](https://github.com/nicetrygee/runway/releases/tag/eval-phase-1a). I'd love to hear how others are turning their agent rules into checks.*
