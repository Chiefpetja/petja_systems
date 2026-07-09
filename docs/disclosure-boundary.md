# Disclosure Boundary

This repository is a public architecture and project overview.

It intentionally does **not** include the full mathematical formulation, internal update rules, detailed reconstruction mechanisms, or sensitive design logic of the experimental systems.

## Why This Boundary Exists

Some parts of the work are intended to remain private research infrastructure.

The public repository should show engineering competence, system boundaries, and honest project status without making the underlying core mechanisms reconstructable.

## Public Content

The repository may include:

- high-level project purpose
- system boundaries
- implementation status
- conservative architecture descriptions
- non-sensitive terminology
- selected run metrics
- reproducible code for public case studies

## Non-Public Content

The repository should not include:

- full mathematical derivations
- core update rules
- internal operator logic
- detailed reconstruction mechanisms
- implementation notes that would allow the core systems to be reconstructed
- private patch history with sensitive design decisions
- diagrams that expose internal mechanism flow

## Exception: Parameter-Golf-inspired Experiment

The Parameter-Golf-inspired GPT training case study is treated separately.

It may include executable code, raw run history, validation metrics, and compressed artefact sizes because this case study is intended as an open, measurable engineering example.

## Practical Rule

The repository should answer:

```text
What is the project?
What is its status?
What problem does it investigate?
What is public and what is intentionally not public?
```

It should not answer:

```text
How can the private core mechanism be reconstructed?
```
