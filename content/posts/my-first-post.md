---
title: Judgement as a System Property
date: 2026-01-22
---  

## Judgement Loops
AI is changing where and how often judgement happens in software engineering.

When implementation becomes significantly cheaper, software engineering stops being a sequence of decisions followed by execution. Instead of one design discussion leading to three days of coding, an engineer might generate and evaluate dozens of alternatives in an afternoon. The cost of trying another approach is close to cheap and the workflow becomes:

Prompt > Review > Refine the prompt > Generate again > Compare alternatives > Accept or reject > Repeat

You're making dozens of smaller decisions throughout the process. It becomes a continuous stream of judgement where every prompt is a design decision. Every generated diff is a trade-off, and every accepted change is a validation of your understanding of the system.

That has an important consequence. Engineering Management doesn't fundamentally change but the density of what it has always been responsible for increases. Imagine a manager responsible for ten engineers. Previously each engineer made perhaps 20 significant engineering decisions a week. Now AI enables each engineer to explore five or ten times as many implementation options.


## Scaling Good Judgement
Some have incorrectly held a belief that Engineering Managers make better decisions than Engineers but that was never true. The role has always been about improving the conditions in which good judgement emerges:

 - improving how judgement is formed.
 - increasing consistency of decision-making.
 - reducing variance across teams.
 - creating systems where good decisions become more likely.

Now that the amount of judgement happening in the org has exploded, the role of the EM shifts from overseeing implementation to scaling good judgement.


## What That Looks Like in Practice
Three capabilities become increasingly critical and frequent:

#### Framing
Poorly framed problems produce incorrect answers faster. AI is very good at optimising for the objective you give it. If that objective is vague, incomplete, or based on the wrong assumptions, AI won't necessarily recognise that and it will confidently generate a solution anyway. Good framing constrains exploration so AI spends less effort exploring irrelevant possibilities and more effort refining solutions that fit your actual problem. The valuable skill is no longer just evaluating generated code. It's correctly defining the problem before any code is even generated.

#### Validation
Cheap output makes accepting incorrect output more expensive. AI makes it very cheap to generate code, documents, designs, and ideas and because output is abundant, people are exposed to far more decisions. If your judgement is poor, you're likely to approve more flawed work. The downstream cost of accepting bad output (bugs, outages, technical debt, security issues, and lost trust) increases because you're making more acceptance decisions than before. The question becomes not can we generate code, but how do we know it's good enough?

#### Coherence
AI accelerates individuals, but also increases divergence in mental models. Maintaining shared understanding becomes more valuable.

That means the manager has to invest more in things like:

 - architectural principles,
 - engineering standards,
 - review practices,
 - prompting skills,
 - system understanding,
 - coaching engineers to evaluate AI output rather than trust it.


## Status Reporting and Delivery Metrics Don't Compress
The need for 'status reporting' (if you want to call it that) has now increased right? The following questions become more frequent and ubiquitous at all levels of experience in your engineering team: at risks have emerged? What decisions need alignment? What trade-offs are you making? Consequently, managers spend more time interpreting signals. 

Just to be clear, the role of an Engineering Manager or a Delivery Manager has never been to collect activity updates. For years, engineering systems have provided visibility into execution through pull requests, deployments, CI/CD signals, ADRs, and production telemetry. The manager's value has always been in interpreting those signals, improving decision quality, and creating the conditions for effective engineering (or delivery).

Onto Delivery Metrics. When delivery speed becomes easier to achieve then system health, reliability and engineering quality become the harder measures to shift the needle on. AI may increase PR throughput, lines of code, or velocity but none of those necessarily mean you're building a better system. EM's are more interested questions like:

 - Are we making the right decisions?
 - Are we accepting the right AI-generated output?
 - Are our engineering standards holding as throughput increases?
 - Are we trading speed for quality appropriately?

I would strongly argue that this is no different to the set of metrics that good EM's have always cared about most:

 - Are engineers making consistently good decisions?
 - Are customers happier?
 - Is the system becoming more reliable?
 - Is technical debt increasing?
 - Are incidents decreasing?
 - Are changes safe?


### The Implication For EM's
AI lowers the cost of execution but raises the cost of poor judgement. More decisions are made, more quickly, with greater consequences.

Engineering Management's role is not to make more decisions, but to create the systems, principles, and culture that make good decisions repeatable.
