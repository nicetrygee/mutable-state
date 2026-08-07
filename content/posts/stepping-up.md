---
title: "Making the Jump to <del>Hyperspace</del> Senior"
slug: "making-the-jump-to-senior"
date: 2026-08-07
draft: false
---

## Notes on making the jump
What follows is a collection of thoughts, drawn from my own experience and opinions, on how mid-level software engineers can make the jump to senior if they choose to.

## Autonomy: Don't wait for the title 
My view is that the constraint on mid-level engineers is scope of ownership rather than ability. A strong mid-level is technically excellent and in my opinion often every bit the equal of a new senior at writing and reviewing code. The difference is the boundary of what they are asked to own: ambiguous calls tend to be escalated by design, higher-stakes decisions are made jointly with someone more senior, and accountability for a poor outcome ultimately rests above them. This is how the level is typically structured, it's by no means a judgment on the person operating in it.

Senior removes that net. The engineer identifies a problem, determines that it is theirs, and owns the result and that includes the consequences of being wrong.

I also think the distinction matters more now because AI tooling is compressing the technical execution gap between the levels. For example,  a mid-level with capable assistance can now produce code that once demanded senior-level fluency. As much of that technical differentiator erodes, judgment, ownership, and the willingness to be accountable become boundary that AI can't erode as well.

Take how far the ownership extends when an agent's output is shipped. Every engineer should approach agent output as a draft, by reviewing it, questioning it, and trying to improve upon it. The distinction between mid and senior isn't the diligence of that review but the reach of the accountability. When agent-authored code causes an incident, who owns the postmortem, the architectural drift, and the decision to have shipped it at all? Stepping into that answer, rather than escalating it, is the line that separates the levels.

An agent learns by reading code. It's never sat in a meeting room so it doesn't know about the architectural debate the team had a few weeks back, or that said solutions were tried before and failed for reasons that never made it into the codebase. That context lives in people's heads, and holding it and deciding what to say and when it matters, is increasingly what senior work is.

What am I saying? If you want to be senior, it's important to start acting like it. Please don't wait for the title. Start taking ownership of problems, making decisions, and being accountable for the outcomes. Show that you can handle ambiguity and complexity, and that you can lead initiatives without needing constant guidance.

## The Glue Work Trap
Sorry. Another Star Wars ref. Facepalm. A big part of stepping up means taking ownership of work that wasn't assigned to anyone and it divides into technical and organizational work. My strong preference is to default to the technical because an engineer's primary responsibility is to ship and maintain code.

The organizational work is the maintaining of the board, onboarding newcomers, writing documentation, coordinating incident communication and this also carries real value. Tanya Reilly terms it glue work, and her caution is important: glue work is expected of seniors and hazardous for non-seniors if they don't carefully balance it. It should be done deliberately and in proportion. An engineer whose entire contribution is glue tends to become indispensable to the team but invisible to promotion unless you have a darn good Engineering Manager or manager who can advocate for you. In my experience, the best way to avoid this trap is to make sure that the glue work is in service of technical work and that the technical work is visible and impactful.

## Where to find the work
The work of stepping up should be more prepared than improvised. Ideas are best sourced from the people already carrying the daily friction such as your teammates, leads, EM's and product managers. Communicate the intent to a manager or lead before commitment, so that the work remains trackable, time-boxed, and aligned to team goals. It should be scoped and decomposed into tickets, so that progress is measurable and the deliverable is visible.

Technical opportunities are consistent across companies. Tests for an under-tested module, added instrumentation, a resolved performance hotspot, or pairing with a newcomer. In an AI-assisted it could be writing the spec that constrains an agent before it generates anything, designing the evals that verify its output against a real signal, and reviewing generated diffs for architectural correctness rather than merely passing tests. Opportunities follow the same pattern: relieving a tech lead of a task, building an onboarding program, standardizing dashboards, or establishing an incident-response path where none exists.


## Sources
The Age of Agentic AI: What Engineering Jobs Actually Look Like in 2026
AI Agents Don't Replace Senior Engineers — They Demand More
AI Code Quality: The Hidden Cost Senior Engineers Pay
Who Owns Engineering Judgment?
Agentic Engineering: Karpathy's New Framework