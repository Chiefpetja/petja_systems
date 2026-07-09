# Public Terminology

This document defines only the public, non-sensitive terminology used in the repository.

## Field Core

The data-side system that transforms tabular datasets into deterministic structural artefacts. Public descriptions should avoid formulas and internal update rules.

## Frequency Bubble Model

The earlier public name for the structural data-analysis direction. In the current public documentation, it is paired with the Field Core name to make clear that the work has moved beyond the older high-level description.

## Structural Artefact

A non-sensitive term for an output produced by the Field Core, such as an interaction summary, zone-like representation, chain-like relation, or local state description.

## Structural Prediction Model

A separate prediction branch that aims to interpret Field Core artefacts for target prediction. It should not be confused with earlier standard-predictor experiments.

## Jarvis Context Engine

A blueprint-to-execution prototype for controlled software iteration. Public descriptions should focus on tests, logs, execution boundaries, and commit gates.

## Crab Router

A deterministic context-growth layer for text/prose inputs. It is intended as a Jarvis extension for making LLM planning more grounded and inspectable.

## Evidence Case Study

A project section that contains measurable experiments, code, and run results. The Parameter-Golf-inspired GPT experiment belongs here.

## Public Naming Rule

Prefer clear functional names over abstract or personal names.

Good public names:

```text
input_builder.py
field_features.py
target_estimator.py
evaluate_mae.py
error_analysis.py
prediction_state.py
```

Avoid names that are too abstract, unexplained, or person-based.
