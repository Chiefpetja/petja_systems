# Structural Prediction Model

## Summary

The Structural Prediction Model is an active development branch for target prediction based on artefacts produced by the Field Core.

It exists because earlier attempts with standard predictors did not work well enough. The raw structural outputs of the Field Core require interpretation before they can be used meaningfully for prediction.

## Public Goal

The goal is to build a prediction layer that can interpret structural artefacts instead of treating them as ordinary feature columns.

At a public level, the direction can be described as:

```text
Field Core artefacts
→ interpretation layer
→ target estimation
→ error analysis
→ iteration
```

## Why a Separate Model Is Needed

The early approach was to take outputs from the Field Core and feed them into standard predictors in order to improve MAE values.

That approach did not provide the expected improvement because the standard predictors did not know how to read the generated structural values. They saw numbers, but not the structural context those numbers came from.

The new direction is therefore not just another standard model on top of exported features. It is a dedicated prediction branch designed to work with the meaning of the artefacts.

## Naming Guidelines

Public names should be direct, functional, and easy to understand.

Recommended naming style:

```text
structural_prediction/
  input_builder.py
  field_features.py
  target_estimator.py
  prediction_state.py
  evaluate_mae.py
  error_analysis.py
```

Avoid names that are:

- too abstract before they are explained
- based on unclear metaphors
- based on the author's name
- suggestive of validated production capability before validation exists

## Public Boundary

The public repository may describe:

- why the branch exists
- what problem it addresses
- how it differs from the deprecated standard-predictor experiments
- its current development status

The public repository should not include:

- formulas
- detailed scoring logic
- reconstruction rules
- internal interpretation mechanics
- private training or update mechanisms

## Status

Active development.

Not yet presented as a validated production predictor.
