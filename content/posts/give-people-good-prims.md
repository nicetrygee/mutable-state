---
title: "Give People Good Primitives"
slug: "give-people-good-primitives"
date: 2026-08-07
draft: false
---

## What's an Orchestrator
You have a set of steps that need to run in order. Some of them fail, some are slow, and you want to see all of them clearly when they break in the middle of the night. The problem with tools I've been exposed to in this space is that they add a second job on top of that. You have to learn their model of the world before you're allowed to describe yours.

## Static vs Dynamic
Prefect removed that. Say you have a Python function that does a thing? Put `@task` on it. You have a function that calls a bunch of those? Put `@flow` on it. That's it. There's no DSL or YAML. Your code is the pipeline. If you've ever spent an afternoon translating working Python into an orchestrator's idea of a DAG then you'll know how liberating that is. Assuming you're not just using an agent.

That design also pays off when your workflows are dynamic, but to be fair Airflow also has dynamic task mapping. For example: query a db, get back an unknown number of files, call `.expand()` and the scheduler creates one task instance per file at runtime. 

What mapping gives you is a variable count of a task you already declared. The shape is fixed up front and only the number moves. The cases that still fight you are the ones where the shape itself is the unknown. I encountered this on a recent project for a client where a loader drained a backlog of batches into a downstream system that had been unavailable for a few hours. Each batch has to finish before the next one starts, because a later batch can carry a newer version of a record the earlier one is still writing, and if batch 4 fails you want the loop to stop rather than push batch 5 on top of it. You don't know how many batches are waiting until you start draining and you don't know whether there's another one until the last commit lands. To the best of my knowledge, mapping can't express that. Mapped instances are siblings that don't know about each other, so a failure in one doesn't stop the rest, and forcing them to run one at a time through concurrency settings gives you the sequencing but without the dependency you actually wanted.

Prefect doesn't have a separate define the graph step. A flow is a Python function that runs top to bottom. There's a `while` loop and `if` really does branch, so the graph emerges as the code executes instead of being locked in beforehand.

## Observability
Retries are an arg and failures show up with the context you need instead of a stack trace to dig into. The UI shows you the shape of a run such as what passed, what's still going, where it died...without you instrumenting your way there. I should caveat this by saying I'm still a big fan of Airflow. I guess Prefect is just a better fit for the way I want to work now. I want to write Python, not YAML.

## Give People Good Primitives
The risk is that Prefect gives your code the benefit of the doubt. It doesn't try to protect you from your own code. I really like the trust though. Give competent people good primitives and clear feedback and maybe they'll build something better than a framework would have prescribed for them?

I'm a keen student of Prefect. By no means a power use and I'm sure it's far from perfect but I love the notion that it respects the work and the people doing it. 