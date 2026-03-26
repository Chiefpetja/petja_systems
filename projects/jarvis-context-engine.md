# Jarvis

Jarvis is an execution and testing engine for structured blueprints.

Its purpose is to transform a structured idea (Blueprint) into minimal executable code, run tests, and generate real feedback.

The system focuses on **fast falsification and iteration** rather than autonomous generation.

---

## Core Principle

Blueprint → Code → Tests → Feedback → Iteration

Jarvis treats every blueprint as a **hypothesis about reality**.  
Reality is validated through tests, linting and type checks.

---

## System Architecture

Jarvis separates thinking, decision making and execution into strict layers.

### Language Center

Responsible for:

- understanding blueprints
- generating structured plans
- defining tool calls

Restrictions:

- cannot execute
- cannot write files

---

### Neural Router

Policy layer that decides:

- which action to perform next
- which tool to use
- which tests to run

This component learns from execution logs and improves routing efficiency.

---

### Execution MAS (Multi-Agent System)

Deterministic execution environment containing specialized agents.

Agents include:

- RepoScout – finds relevant code locations
- PatchAgent – generates code changes as diffs
- TestRunner – executes tests and validation
- DebugAgent – interprets failures
- CommitGate – controls all write operations

---

## Safety Model

All code modifications must pass through **CommitGate**.

CommitGate guarantees:

- snapshot before write
- full audit log
- blocked unsafe actions

---

## Execution Loop

1. Blueprint is provided
2. Language Center generates plan
3. Neural Router selects action
4. Execution agents perform tasks
5. Tests validate results
6. Failures trigger debug iteration
7. Passing tests allow commit

---

## Design Philosophy

Jarvis is not an autonomous AI developer.

It is closer to a **deterministic compiler for blueprints**, where:

- the blueprint is the hypothesis
- execution is the experiment
- tests define truth

---

## Status

Jarvis is currently under active development.

The execution architecture is stable, but integration with the Crab Router exploration layer is still pending due to unresolved issues related to LLM attractor behavior during planning.