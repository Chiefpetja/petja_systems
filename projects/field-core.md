# Field Core / Frequency Bubble Model

## Summary

The Field Core is a deterministic structural analysis pipeline for tabular datasets.

It transforms input data into internal structural artefacts that can be inspected, compared, and used by separate downstream analysis or prediction layers.

## Public Role

The Field Core belongs to the data / structure side of the project map.

At a public level, the system can be described as:

```text
Tabular dataset
→ structural data preparation
→ interaction summaries
→ zone-like representations
→ chain-like relations
→ local state artefacts
→ diagnostics / downstream use
```

The system is not presented as a direct prediction model. Its purpose is to build a structural representation of a dataset, not to output target estimates by itself.

## Current Position

The current core is newer than the earlier public Frequency Bubble Model description.

Older descriptions focused on general ideas such as structural clusters, stability regions, and interaction flows. The current implementation should be described more conservatively as a structural artefact generator with deterministic processing stages.

## What Can Be Publicly Said

The public repository may describe that the core produces artefacts such as:

- interaction summaries
- zone-like representations
- chain-like relations
- local state descriptions
- diagnostic outputs for downstream work

These terms are intentionally high-level. They describe the category of output without exposing the underlying mechanism.

## Deprecated Predictor Experiments

Some older snapshots included early predictor experiments that attempted to extract better MAE values from Field Core outputs using standard prediction models.

Those experiments are not the current prediction direction.

The main problem was that standard predictors treated the generated structural numbers like ordinary raw feature columns. They could not reliably interpret what those numbers meant inside the Field Core representation.

That result led to the separate Structural Prediction Model branch.

## Current Boundary

The Field Core documentation should remain high-level.

Do not include:

- mathematical formulas
- internal update rules
- reconstruction details
- operator logic
- patch-level design history
- diagrams that expose internal mechanism flow

The public goal is to show that a real structural analysis core exists and has a clear boundary, not to disclose how it works internally.

## Status

Active technical core.

Public documentation should present the system as ongoing experimental infrastructure, not as a finished library or validated commercial product.
