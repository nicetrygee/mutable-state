---
title: "Who Gets to Build Software?"
date: 2026-11-24
draft: true
---

## What if the next generation of great software builders aren't software engineers?
Before the engineers reach for their pitchforks, I'm not suggesting that engineering expertise is becoming redundant. Quite the opposite. Building reliable, secure and maintainable software requires deep technical knowledge, experience and judgement. AI doesn't magically remove that complexity. In some respects, it makes that expertise even more important but it's hard to deny that something fundamental is changing.

AI has removed the barriers between having an idea, exploring a solution and actually building it quickly and to a decent standard. People who understand problems exceptionally well, but have never written a line of production code, can now increasingly participate in designing, prototyping and constructing software.

## Tradition
For decades, software development has operated around a fairly well-established division of responsibilities. Product managers identify opportunities and define what needs to be built. BA's translate those needs into requirements. Delivery managers coordinate the work. Engineers interpret the requirements, make technical decisions and build the software. QA's and Ops help ensure it works and remains reliable.

There are good reasons for this division. Building software requires specialist knowledge, considerable technical experience and an understanding of the complexities that sit beneath seemingly simple requirements. But AI is absorbing an growing proportion of the work that traditionally necessitated those boundaries

I've been exploring combining two approaches: Spec-Driven Development (SDD) and Amazon's AI-Driven Development Lifecycle (AI-DLC). Together they suggest something considerably more transformative: a potential shift in who can participate in engineering, how software gets built and where the value of an engineering org actually resides.

## AI-DLC
Amazon's AI-Driven Development Lifecycle (AI-DLC) is a framework for building software with AI agents. There's very little that's ground breaking about it but the premise is spot on. Our existing SDLC methods, are designed for human-driven, long running processes, with product owners, developers, architects alike spending most of their time on planning, meetings, and other rituals. Simply retrofitting AI as an assistant not only constrains its capabilities but also reinforces outdated inefficiencies. To truly harness AI’s power and productivity, we need to reimagine our SDLC, and the more interesting implications emerge when we consider what happens to the people involved.

## Lowering the barriers to participating in engineering
SDD provides a structured way to communicate intent, constraints and expected behaviour. AI-DLC provides a workflow through which that intent can be translated into software and this creates an interesting possibility. Someone who understands a business problem exceptionally well, but has limited coding experience, can participate in engineering much earlier and more meaningfully. A product manager might describe a customer problem, work with AI to explore alternative solutions, generate functional designs, develop prototypes and validate assumptions with users. A delivery manager might help decompose a business outcome into independently deliverable components, explore dependencies, coordinate agent execution and monitor progress against agreed specs.

I'm not saying anyone can become a software engineer by prompting an AI. We're lowering the barrier to participating in engineering, not necessarily lowering the bar for engineering quality. The emerging skill set becomes less exclusively about programming and more about problem decomposition, systems thinking, understanding constraints, evaluating trade-offs and validating outcomes. These aren't exclusively engineering skills. Good product managers, business analysts and delivery managers already exercise many of them.

## Product people become solution builders
Today, a product manager might identify an opportunity, produce a business case, create a roadmap and write user stories. They then wait for engineering to turn those things into reality. With SDD and AI-DLC, that relationship changes considerably. A product manager or someone with a similar skill set cannow:

 - Describe a problem and desired outcome.
 - Work with AI to explore possible solutions.
 - Generate competing functional designs.
 - Build working prototypes.
 - Test assumptions with users.
 - Refine the spec based on feedback.
 - Initiate implementation through engineering agents and skills.
 - Monitor whether the delivered solution achieves its intended outcome.

Product management is now continuous solution discovery and construction. The product manager is no longer limited to describing what should be built. Importantly, this doesn't mean PMs should independently approve production architecture, security decisions or operational readiness. It means they can get much closer to the solution without first having to become professional software developers.

## Delivery managers become engineering orchestrators
Traditional delivery management spends a considerable amount of time coordinating human capacity. For example, who is available? What are they working on? What are the dependencies? What's blocked? What can be delivered next? What's the impact of changing priorities? Some of this coordination exists because humans are expensive, specialised and difficult to synchronise. 

AI-DLC introduces the possibility of a different operating model where a delivery manager works with agents to decompose outcomes into Units of Work, identify dependencies, explore alternative implementation strategies, coordinate parallel workstreams and monitor progress against specifications. Instead of primarily tracking the production of engineering artefacts, they manage the flow of value through an increasingly agentic engineering system.

This moves delivery management away from coordinating activity and towards orchestrating outcomes. It also makes the role considerably more technical and potentiallymore valuable. The delivery manager doesn't need to be the person implementing the solution. They need to understand how the solution is decomposed, what needs to happen, what could go wrong and how the different components come together.

## Engineering becomes more about judgement than production
This is probably the biggest organisational implication. If AI increasingly handles implementation, a scarcer resource becomes the ability to determine whether the proposed technical solution is actually right. The ability to recognise a bad solution, challenge an assumption, understand a system-level implication or identify an architectural risk becomes increasingly valuable. AI doesn't make engineering expertise redundant. It potentially makes that expertise available at a different point in the process, where it can have greater leverage.

## The challenges we shouldn't underestimate
*The illusion of understanding*: AI makes it remarkably easy to produce something that looks technically sophisticated. Someone with limited engineering experience can generate an application, complete with an architecture, database schema and API design, without necessarily understanding the implications. Being able to generate an architecture isn't the same as understanding its trade-offs.

*Spec bureaucracy*: SDD could inadvertently recreate Waterfall with an AI-generated documentation factory.Requirements specs, functional specifications, technical specs, architecture specs, test specs and implementation plans could become increasingly elaborate without necessarily adding value. The objective should be sufficient context to execute safely, not maximum documentation. Specs need to be proportional to risk and complexity.

*Who is accountability?*: If a product manager can generate an application, who is responsible when it exposes sensitive customer data, corrupts production records or becomes impossible to maintain? The ability to initiate software development shouldn't automatically confer the authority to release software into production. We need clear boundaries around who can initiate, construct, validate and approve solutions. Democratising the ability to build is not the same as decentralising responsibility for production systems.

## What I think the future engineering org looks like
*The Product Builder*: Owns the problem, explores solutions, develops prototypes, tests hypotheses and validates outcomes. Their strengths are product discovery, systems thinking, specification, experimentation and technical literacy.

*The Engineering Orchestrator*: Owns the flow of work across humans and agents, manages dependencies, coordinates execution and provides visibility of delivery risks. Their strengths are decomposition, sequencing, agent orchestration, risk management and systems thinking.

*The Technical Authority*: Owns architectural integrity, technical decisions, quality standards, security, reliability and the long-term health of the system. Their strengths are architecture, technical judgement, verification, integration and operational engineering.

## Final thought
The opportunity isn't to replace engineering with AI. It's to make engineering something many more people can meaningfully participate in, while retaining the expertise and accountability required to do it well.
