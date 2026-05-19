---
title: On Engineering Teams and Mutable State
tagline: What software taught me about managing people
date: 2025-05-15
---

The analogy I keep coming back to is this: managing an engineering team is less like writing a program and more like maintaining one that's already running in production.

You didn't write most of the code. Some of it is undocumented. Parts of it are brilliant. Other parts make you wince. And you can't just stop the world and rewrite it — the system has to keep running while you improve it.

### State is everywhere

In software, *mutable state* is the source of most complexity. A variable that can change over time is harder to reason about than one that can't. You have to track not just what it is, but what it was, what it will be, and who might be changing it right now.

People are exactly like this. They carry history. They have context you don't have. They change — sometimes slowly, sometimes suddenly. And unlike variables, they change *themselves*, often in response to being observed.

### The temptation of immutability

There's a reason functional programming has appeal. If nothing changes, everything is predictable. Deterministic. Easy to test.

Some managers try this. They over-specify, over-process, and over-document in an attempt to make their team behave like a pure function: same input, same output, every time.

It doesn't work. You end up with a system that's rigid, slow to adapt, and full of people who've stopped thinking for themselves.

### Working with the state you have

The better approach is to understand the state, not eliminate it. Know where the complexity lives. Know which parts of your team are stable and which are in flux. Build systems that handle change gracefully rather than ones that pretend change won't happen.

Mutable state isn't the enemy. Unobserved mutable state is.
