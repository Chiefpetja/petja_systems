# Petja Systems

Public architecture and project overview for experimental systems around controlled execution, deterministic context growth, structural data analysis, and measurable machine-learning experiments.

This repository is intentionally written as a **showcase and status overview**. It documents project direction, system boundaries, implementation status, and selected evidence without disclosing private mathematical formulations or sensitive internal mechanisms.

## Project Map

The current work is separated into three public areas:

```text
Petja Systems
├─ Text / Planning Side
│  ├─ Jarvis Context Engine
│  └─ Crab Router
├─ Data / Structure Side
│  ├─ Field Core / Frequency Bubble Model
│  └─ Structural Prediction Model
└─ Evidence Case Studies
   └─ Parameter-Golf-inspired GPT training
```

The split is intentional:

- **Jarvis** and **Crab Router** belong to the text, planning, execution, and validation side.
- **Field Core** and the **Structural Prediction Model** belong to the data, structure, and prediction side.
- **Parameter-Golf-inspired GPT training** is included as an open evidence case with code and measurable run logs.

## Projects

### Field Core / Frequency Bubble Model

A deterministic structural analysis pipeline for tabular datasets.

The Field Core transforms input data into internal structural artefacts that can be inspected, compared, and used by separate downstream layers. It is not presented as a classical clustering method and is not presented as a prediction model.

The public repository only describes the role, boundaries, and current status of the system. The mathematical formulation, internal update rules, and detailed reconstruction mechanisms are intentionally not included.

See: [`projects/field-core.md`](projects/field-core.md)

### Structural Prediction Model

An active development branch for target prediction based on artefacts produced by the Field Core.

Earlier experiments tried to feed raw Field Core outputs into standard prediction models to improve error metrics. That direction did not work well enough because the standard predictors treated the outputs as ordinary numeric columns and could not reliably interpret their structural meaning.

The current direction is therefore a dedicated prediction layer that is designed around the artefacts instead of treating them as raw feature values.

See: [`projects/structural-prediction-model.md`](projects/structural-prediction-model.md)

### Jarvis Context Engine

A conservative blueprint-to-execution prototype.

Jarvis is intended to turn structured software blueprints into controlled execution loops with tests, logs, and explicit write boundaries. It is not presented as an autonomous AI developer.

See: [`projects/jarvis.md`](projects/jarvis.md)

### Crab Router

An experimental deterministic context-growth layer for text and prose inputs.

The goal is to explore whether controlled context expansion can make LLM planning more grounded and reduce hallucination risk. Crab Router is intended as a possible extension for Jarvis.

See: [`projects/crab-router.md`](projects/crab-router.md)

## Evidence Case Study

### Parameter-Golf-inspired GPT Training

A measurable GPT training experiment inspired by OpenAI's Parameter Golf challenge format.

This is **not an official competition submission** and is not presented as a leaderboard result. The challenge format was used as a reference environment for constrained training experiments with executable code, run history, validation metrics, and compressed artefact sizes.

Unlike the core research systems, this case study intentionally includes code and raw run logs.

See: [`case-studies/parameter-golf/README.md`](case-studies/parameter-golf/README.md)

## Disclosure Boundary

This repository intentionally avoids publishing the private research core.

Public documentation may include:

- project purpose and motivation
- high-level architecture boundaries
- implementation status
- conservative descriptions of system roles
- selected non-sensitive artefact categories
- public case-study code and run metrics

Public documentation should not include:

- mathematical derivations of the core systems
- internal update rules
- detailed reconstruction mechanisms
- private patch history with sensitive design decisions
- diagrams that expose internal mechanism flow
- implementation notes that would allow private mechanisms to be reconstructed

See: [`docs/disclosure-boundary.md`](docs/disclosure-boundary.md)

## Repository Structure

```text
README.md
projects/
  field-core.md
  structural-prediction-model.md
  jarvis.md
  crab-router.md
case-studies/
  parameter-golf/
    README.md
    train_gpt_runpod.py
    run_history.csv
docs/
  disclosure-boundary.md
  status-matrix.md
  terminology.md
```

## Status

This repository is a public overview of ongoing experimental work. The projects are at different maturity levels and are described conservatively in the status matrix.

See: [`docs/status-matrix.md`](docs/status-matrix.md)

## Author

Independent developer focused on system architecture, structured problem solving, experimental software systems, and evidence-driven iteration.

The goal of this repository is to present a clear public view of the work without exposing private research mechanisms.
