---
title: Engineering Management in the Age of Continuous Judgement
tagline: Constant decisions, constant cost.
date: 2026-01-22
---  


There’s a subtle but important misunderstanding emerging in how people talk about AI in software engineering. It’s often framed as a shift in productivity, or maybe even a shift in roles with engineers becoming more like managers. But in my opinion that framing misses the deeper change.

AI is not primarily changing who does the work. It is changing the structure in which judgement is exercised because when execution becomes super cheap and fast, engineering stops being a sequence of discrete decisions followed by implementation. Instead, it becomes a continuous stream of judgement. Every prompt is a design choice. Every generated diff is a trade-off. Every acceptance is a validation of system understanding.

All of this has a quiet consequence. Engineering Management is no longer operating in a world where judgement is episodic and distributed through hierarchy. It's now operating in a world where judgement is continuous, embedded, and high-frequency across every layer of the system. That changes the nature of the role, not by elevating it or diminishing it, but by increasing the density of what it has always been responsible for improving.


### Engineering management was never about ownership of judgement
A common simplification is to describe Engineering Managers (EM's) as people who “make better decisions” than engineers. That was always inaccurate and lazy. In strong engineering orgs, EM's have always been responsible for something more subtle:  

- improving how judgement is formed
- increasing the consistency of decision-making
- reducing variance in interpretation across a team
- creating systems where good decisions are more likely to happen


In other words, EMs were never the source of judgement. They were part of the system that shaped its quality and this distinction matters more now than it used to because AI doesn't remove judgement from engineers or concentrate it in management. It increases the number of moments where judgement is required and collapses the time between those moments.  

### The collapse of the implementation buffer

Historically, software engineering had a natural buffer between judgement and consequence.   

Design ->  implement -> discover issues during build or integration -> iterate.  

Execution acted as a delay mechanism; absorbing uncertainty. AI now compresses that buffer where implementation is near instant. Alternative solutions are cheap to generate. System changes propagate quickly. Building becomes the default mode of reasoning, and this removes the reflection layer that previously sat between decision and outcome. As a result, judgement becomes continuous rather than staged, and that shifts the cognitive structure of the discipline.


### What changes in practice
In an environment of continuous judgement, EM work becomes less about discrete coordination and more about system calibration. Three areas become dominant:

1. Framing quality - 
How problems are defined before they enter AI-assisted workflows becomes critical. Poor framing produces fast wrong answers. Good framing produces constrained, useful exploration.

2. Validation density - 
Because output is cheap, the cost of accepting incorrect or subtly wrong output increases. EMs become more involved in shaping what “correct enough” actually means in practice.

3. Cognitive coherence across teams - 
As AI accelerates individual throughput, divergence between mental models increases. Maintaining shared understanding becomes harder, not easier.

None of these are new responsibilities but all of them become higher frequency and higher consequence.


### The compression of traditional coordination
I believe that some parts of engineering management don't scale upward in this new model. They compress:

  - task breakdown becomes automated or implicit
  - status reporting loses value when work is continuously visible
  - micro-coordination is absorbed into tooling and workflows
  - delivery tracking becomes less informative than system health signals

This doesn't eliminate management but it does remove a layer of management that was previously necessary due to the execution buffer. What remains is higher leverage, but also less surface area.



### The uncomfortable implication
The most important shift is not that EM's become more strategic or more technical. It's that the cost of poor judgement has increased faster than the exclusivity of judgement itself. This creates a new pressure where engineers exercise judgement more frequently. AI increases the plausibility of incorrect outputs and systems evolve faster than human verification cycles.

In this environment, the value of engineering management becomes less about directing work, and more about stabilising the quality of judgement under speed. Not through control but through shaping environments where good judgement is more likely to emerge repeatedly. The stuff we do all day everyday. Just at scale.


### Closing thoughts
Judgement is no longer a role-specific capability. It's a system property. It emerges continuously from the interaction between engineers, AI systems, and org structure. EM's become less like coordinators of work, and more like designers of judgement conditions. Their influence moves from decisions to decision environments. The role doesn't disappear but it becomes less about managing flow, and more about managing coherence under continuous generation.