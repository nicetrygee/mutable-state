---
title: "An Ode to Prefect"
slug: "an-ode-to-prefect"
date: 2026-08-07
draft: false
---

## What's an Orchestrator
You have a set of steps that need to run in order. Some of them fail, some are slow, and you want to see all of them clearly when they break in the middle of the night. The problem with tools I've been exposed to in this space is that they add a second job on top of that. You have to learn their model of the world before you're allowed to describe yours.

## Static vs Dynamic
Prefect removed that. Say you have a Python function that does a thing? Put @task on it. You have a function that calls a bunch of those? Put @flow on it. That's it. There's no DSL or YAML. Your code is the pipeline. If you've ever spent an afternoon translating working Python into an orchestrator's idea of a DAG then you'll know how liberating that is. 

That design also pays off when your workflows are dynamic. In the Airflow model, you define the DAG up front, as a fixed structure before the workflow runs. Airflow reads that definition, builds the graph, and then schedules it. The shape of the work has to be known in advance. That's fine until your workflow becomes dynamic. Say you query a db and get back an unknown number of files, and you want one task per file. You don't know how many that is until the query runs which is after the point where Airflow wanted the graph fixed. That's a runtime decision, and the fixed-graph model kind of fights you on it.

Prefect doesn't have a separate "define the graph" step. A flow is just a Python function that runs top to bottom. So a for loop over your query results really is a loop. It spawns however many tasks the data calls for. The graph emerges as the code executes, instead of being locked in beforehand.

## Observability
Retries are an arg and failures show up with the context you need instead of a stack trace to dig into. The UI shows you the shape of a run such as what passed, what's still going, where it died...without you instrumenting your way there. I should caveat this by saying I'm still a big fan of Airflow. I guess Prefect is just a better fit for the way I want to work now. I want to write Python, not YAML.

## Give People Good Primitives
The risk is that Prefect gives your code the benefit of the doubt. It doesn't try to protect you from your own code. I really like the trust though. Give competent people good primitives and clear feedback and maybe they'll build something better than a framework would have prescribed for them?

I'm a keen student of Prefect. By no means a power use and I'm sure it's far from perfect but I love the notion that it respects the work and the people doing it. 