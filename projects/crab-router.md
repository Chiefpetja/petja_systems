# Crab Router

## Summary

Crab Router is an experimental context-growth layer for text and prose inputs.

It was developed as a possible extension and redesign direction for Jarvis. Its purpose is to explore whether a natural-language blueprint can first be transformed into a bounded internal coherence landscape before it is handed to an execution system.

The core idea is not to immediately force a blueprint against external reality. Instead, Crab Router treats the blueprint as a self-contained context space in which possible interpretations, assumptions, task frames, and solution attempts can emerge in a controlled way.

At a public level, the intended direction is:

```text
text / prose blueprint
→ deterministic segmentation
→ bounded context growth
→ internal coherence landscape
→ candidate task frames
→ comparison between internal states
→ selected state
→ execution handoff
```

Crab Router is therefore not presented as a finished hallucination-prevention system. It is better understood as an experimental containment layer for speculative context construction.

The goal is to make internal exploration more explicit, comparable, and auditable before an execution system such as Jarvis tests anything against external reality.

## Core Assumption

The core assumption behind Crab Router is that a blueprint can be treated as a self-contained coherence space.

A blueprint does not immediately have to be checked against external reality in order to be useful. Before execution begins, it can first be expanded into an internal context landscape where possible interpretations, assumptions, task frames, and solution attempts are allowed to emerge in a controlled way.

Within this landscape, the system can perform bounded exploration.

The goal is not to prevent every hallucination or speculative construction at the moment it appears. The goal is to keep uncertain constructions inside a controlled context space, preserve where they came from, and compare them against other internally generated states.

At this stage, a candidate is not judged by whether it is already externally true. It is judged by whether it remains coherent inside the blueprint-derived landscape.

```text
blueprint
→ bounded context landscape
→ candidate interpretations
→ internal coherence comparison
→ selected state for downstream execution
```

External validation comes later.

In the broader architecture, Crab Router prepares a more coherent and inspectable state. Jarvis or another execution layer can then test that state against external reality through tools, code, tests, runtime checks, and feedback.

The assumption is therefore:

```text
controlled internal exploration first
→ external validation later
```

This does not mean that internal coherence proves correctness. It only means that before a system acts on the outside world, its generated context should be made explicit, comparable, and internally stable.

## Motivation

Natural-language blueprints are useful because they are flexible.

They can describe goals, constraints, examples, priorities, edge cases, non-goals, and open questions in one place. But this flexibility also makes them unstable as direct execution input.

A blueprint may contain:

- instructions
- assumptions
- constraints
- definitions
- examples
- open questions
- unresolved ambiguities
- competing interpretations

If all of this is passed directly into an LLM as one continuous prompt, it can be difficult to know which parts were preserved, which parts were ignored, which interpretations were created, and which assumptions influenced the final plan.

Crab Router was built to investigate a stricter approach:

- segment the blueprint into context-bearing units
- grow context step by step
- preserve origin references
- allow bounded internal exploration
- compare candidate states against the blueprint-derived context
- produce structured task frames
- hand execution intent forward through explicit envelopes
- collect feedback as structured artefacts
- identify gaps, collisions, or unresolved parts of the context landscape

The goal is not to remove speculation from the planning process.

The goal is to keep speculation contained, inspectable, and comparable before anything is executed.

## Public Concept

Crab Router can be understood as a context-construction pipeline.

The public version can be described like this:

```text
document blocks
→ blueprint units
→ context snapshots
→ context frames
→ candidate task frames
→ internal comparison
→ selected task state
→ execution envelope
→ feedback and audit artefacts
→ gap requests
```

The important design choice is that the system tries to preserve context history.

Each step should make it possible to ask:

```text
Where did this interpretation come from?
Which part of the blueprint created it?
Which context existed at that point?
What was allowed to vary?
What was fixed?
What was unknown?
Which candidate states were created?
Why was one state selected over another?
What still needs external validation?
```

This makes the system less like a free-form conversation and more like an append-only context and task construction process.

## Internal Exploration vs. External Validation

Crab Router separates two phases that are often mixed together.

### 1. Internal Exploration

The system first builds a blueprint-derived context landscape.

Inside this landscape, multiple candidate interpretations or task states can be created and compared. These candidates do not need to be externally proven yet. They only need to remain traceable and internally coherent with the blueprint-derived context.

This phase is about controlled exploration.

```text
blueprint context
→ candidate states
→ internal comparison
→ coherence selection
```

### 2. External Validation

Only after a state has been selected does it become useful as execution input.

At that point, another system can test it against external reality.

For software work, this may include:

- repository inspection
- tool calls
- code execution
- tests
- linting
- type checks
- runtime feedback
- human review

This phase is about reality contact.

```text
selected state
→ execution system
→ external checks
→ feedback
```

Crab Router is focused mainly on the first phase. Jarvis is intended to handle the second phase more directly.

## What Has Been Built

The available implementation snapshot contains an early pipeline for turning structured document material into run artefacts.

At a high level, the implemented direction includes:

- segmentation of blueprint material into context units
- chronological context growth
- context snapshots as an audit layer
- generation of local context frames
- task-frame construction
- candidate subgoal generation
- execution-envelope construction for Jarvis-style handoff
- feedback recording
- extraction of signal-like information from feedback and execution traces
- construction of a context-network-like artefact
- collision or conflict detection
- assembly gates for checking whether artefacts can be accepted
- timeline reconstruction for run inspection
- context-gap requests for missing or unresolved information

The current public status can be summarized as:

```text
implemented early context pipeline
→ structured run artefacts
→ audit trail
→ bounded context exploration
→ execution handoff concept
→ feedback and gap-detection layer
```

This should still be described conservatively.

The existence of an implementation snapshot does not mean the approach is complete, validated, or ready for production use.

## Relationship to Jarvis

Crab Router is intended as a possible extension or redesign direction for the context-building part of Jarvis.

Jarvis originally focuses on controlled execution:

```text
structured task
→ controlled execution
→ tests / validation
→ feedback
→ commit gate
```

Crab Router focuses on what happens before that:

```text
prose blueprint
→ bounded context landscape
→ candidate task states
→ selected execution state
```

The intended relationship is therefore:

```text
Crab Router
→ prepares a more coherent and inspectable internal state

Jarvis
→ executes and validates the resulting structured task externally
```

The integration should be understood as a design direction, not as a finished combined system.

## Why This Matters

Crab Router is useful as a research direction because it targets a difficult part of LLM-assisted work: the transition from prose to reliable execution context.

A model may fail not only because it generates the wrong answer, but because the context it operates on was already unstable, incomplete, or mixed together in the wrong way.

Crab Router tries to make this transition more explicit.

Instead of asking a model to directly solve a blueprint, it asks whether the blueprint can first be transformed into a bounded context landscape where possible interpretations are allowed to emerge, but remain contained and comparable.

The value of the system is therefore not just in routing tasks.

The value is in making the route itself visible:

```text
not direct answer generation
but visible context construction
```

This creates a clearer separation between:

```text
internal coherence
external correctness
```

Both matter, but they are not the same thing.

## What Crab Router Is Not

Crab Router is not currently presented as:

```text
a finished hallucination-prevention system
a production-ready planning framework
a replacement for human review
a complete autonomous reasoning system
a guarantee that LLM output is correct
a proof that internally coherent states are externally true
```

It is an experimental context-growth and planning-support layer.

Its purpose is to test whether bounded internal context construction can make downstream LLM-assisted execution more inspectable and less error-prone.

## Current Status

Crab Router is currently best described as:

```text
concept / early implementation direction
```

The current project state describes an early context pipeline with multiple artefact stages and a run-inspection direction.

The public status can be summarized as:

```text
text/prose input
→ deterministic segmentation
→ bounded context growth
→ internal coherence landscape
→ task framing
→ execution handoff artefacts
→ feedback and audit artefacts
→ gap/collision inspection
```

The main open question is whether this explicit context-growth process can measurably improve the reliability of LLM-assisted planning and execution.

## Public Disclosure Boundary

The public repository can describe the motivation, context-growth idea, relationship to Jarvis, and high-level artefact flow.

It does not need to expose:

- private prompt strategies
- internal routing heuristics
- unstable implementation details
- speculative reasoning mechanisms
- detailed internal packet schemas
- claims that hallucinations are solved
- claims that internal coherence proves external correctness

The goal of this document is to explain why Crab Router exists and how it is intended to support Jarvis, while keeping the public description conservative and technically honest.
