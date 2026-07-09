# Jarvis Context Engine

## Summary

Jarvis is a conservative blueprint-to-execution prototype for structured software work.

The original idea behind Jarvis was to take a user-provided blueprint, segment it into a structured execution plan, and then move the remaining process into an auditable system of explicit JSON packets, tool roles, logs, tests, and commit gates.

A language model is only intended to be used at the beginning of the process, where natural-language input has to be understood and converted into a structured plan. After that point, the system should avoid free-form reasoning as much as possible and operate through explicit state packets and controlled execution steps.

At a public level, the intended loop is:

```text
blueprint
→ LLM-assisted segmentation
→ structured JSON task packets
→ controlled execution
→ tests / lint / type checks
→ feedback packets
→ gated commit
```

Jarvis is therefore not presented as an autonomous AI developer. It is better understood as an experimental execution and validation layer that tries to make LLM-assisted software work more inspectable, auditable, and deterministic.

## Core Assumption

The core assumption behind Jarvis is that natural language is useful for describing intent, but too unstable to serve as the only control layer for software execution.

A blueprint may start as prose, but once it enters the system it should be converted into explicit structured state.

From that point on, the goal is to reduce ambiguity:

```text
prose intent
→ structured task packets
→ deterministic tool calls
→ observable logs
→ validation results
```

The system treats the blueprint as a hypothesis, not as a finished solution.

A proposed implementation only becomes meaningful after it has been executed, tested, and compared against observable feedback.

## Motivation

LLM-assisted programming can be powerful, but it also introduces a specific risk:

A model can produce output that sounds coherent while still being wrong, incomplete, unsafe, or inconsistent with the existing repository.

This becomes especially problematic when planning, execution, debugging, and committing are all mixed into one free-form loop.

Jarvis was designed to investigate a stricter structure:

- use language models for initial understanding and segmentation
- convert the result into explicit structured packets
- keep execution steps inspectable
- make file changes auditable
- use tests and validation as reality checks
- prevent direct uncontrolled writes
- keep a log of what happened and why

The purpose is not to remove the language model from the workflow. The purpose is to limit where it is trusted.

## Public Concept

At a high level, Jarvis separates the workflow into two phases.

### 1. Language Phase

The language phase handles the initial blueprint.

Its role is to understand the user's intent and convert it into structured execution material.

This may include:

- segmenting the blueprint
- identifying goals
- extracting tasks
- defining constraints
- producing structured JSON packets

The language phase should not directly modify the repository.

### 2. Execution Phase

The execution phase works on structured packets instead of open-ended prose.

Its role is to inspect the repository, run tools, apply controlled changes, collect results, and produce feedback.

The intended flow is:

```text
JSON task packet
→ tool selection
→ repository inspection
→ patch proposal
→ validation
→ feedback packet
→ commit gate
```

This separation is the central idea of Jarvis.

The LLM helps convert the blueprint into structure, but the system should then operate through explicit packets and validation steps.

## Intended Architecture

The public architecture can be described through four main roles.

### Blueprint Segmentation

The starting point is a natural-language or semi-structured description of what should be built, changed, investigated, or tested.

The first step is to transform that input into a structured representation.

The output should be explicit enough to be inspected and logged.

### Packet-Based Task Handling

After segmentation, tasks are represented as structured packets.

The exact internal packet format is not part of the public documentation, but the public idea is simple:

```text
task intent
constraints
target files or modules
required checks
execution status
feedback
```

This makes the workflow easier to audit than a continuous free-form conversation.

### Controlled Execution

Execution should happen through defined tool roles.

Publicly, this can include roles such as:

- repository inspection
- patch generation
- test execution
- failure analysis
- validation reporting
- commit gating

The important point is not the exact agent names, but the separation of responsibilities.

### Reality Gates

Reality gates decide whether a change can move forward.

Examples include:

- tests
- linting
- type checks
- build results
- runtime validation
- explicit review before commit

A change that sounds correct but fails validation should not be treated as complete.

## What Has Been Built

Jarvis currently exists as an architecture and prototype direction rather than a finished production system.

The original implementation direction focused on building a controlled execution environment around structured task packets.

The public status can be summarized as:

```text
blueprint input
→ initial LLM-assisted segmentation
→ structured task packets
→ controlled execution model
→ validation feedback
→ commit-gate concept
```

This should be described conservatively.

Jarvis is not a finished autonomous coding system. It is an experimental attempt to make software execution more auditable after the initial language-understanding step.

## Relationship to Crab Router

Crab Router is intended as a possible later extension or redesign direction for the context-building part of Jarvis.

The Jarvis description here reflects the original architecture idea:

```text
LLM-assisted blueprint segmentation
→ structured packets
→ controlled execution
```

Crab Router explores whether the context-building step itself can be improved through deterministic context growth before execution begins.

That newer direction belongs in the Crab Router documentation and is not explained in detail here.

## Why This Matters

Jarvis is useful as a project direction because it focuses on a weakness of many AI-assisted coding workflows:

They often produce answers faster than they produce proof.

Jarvis tries to make the path from idea to change more explicit.

Instead of allowing a model to directly move from prose to code to commit, the workflow is split into structured stages:

```text
understand
→ segment
→ packetize
→ execute
→ validate
→ commit only through a gate
```

The value of the system is not just in generating code.

The value is in making the process inspectable enough that mistakes, failed assumptions, and unsafe changes can be detected earlier.

## What Jarvis Is Not

Jarvis is not currently presented as:

```text
a production-ready AI developer
a fully autonomous coding system
a replacement for human review
a guarantee that generated code is correct
a finished multi-agent framework
```

It is an experimental architecture and prototype direction for structured, auditable software execution.

## Current Status

Jarvis is currently best described as:

```text
conservative prototype / original architecture
```

The original direction is defined, but the system should not be described as production-ready.

The public status can be summarized as:

```text
initial blueprint segmentation
→ packet-based execution idea
→ validation-first design
→ commit-gate concept
→ context-building improvements moved toward Crab Router exploration
```

## Public Disclosure Boundary

The public repository can describe the motivation, architecture, role separation, packet-based workflow, and validation-first design of Jarvis.

It does not need to expose:

- private planning prompts
- internal packet schemas
- unfinished implementation details
- speculative agent behavior
- claims of autonomy that are not validated

The goal of this document is to explain why Jarvis exists and how it was intended to structure software execution, while keeping the public description conservative and technically honest.
