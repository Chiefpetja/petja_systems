# Parameter-Golf-inspired GPT Training

## Summary

This is a measurable GPT training experiment inspired by OpenAI's Parameter Golf challenge format.

It is **not an official competition submission** and is not presented as a leaderboard result. Some constraints were relaxed during development to explore architecture changes, debug training behavior, and collect measurable engineering evidence.

## Why It Is Included

Most projects in this repository are described conservatively and without exposing internal research mechanisms.

This case study is different: it is included as an open evidence block with executable code and raw run metrics.

The value is the measurable development loop:

```text
architecture change
→ training run
→ validation loss / BPB
→ compressed artefact size
→ next iteration
```

## Included Files

```text
train_gpt_runpod.py   # executable training script
run_history.csv       # raw logged runs and metrics
```

## Selected Observed Runs

These values are taken from the raw run history. They should be read as experimental engineering logs, not official competition records.

| Run label | Wall-clock setting | Steps reached | Validation loss | BPB | int8+zlib bytes | Status |
|---|---:|---:|---:|---:|---:|---|
| baseline local | 600s | 863 | 2.8101 | 1.6643 | 11,817,558 | constraint-close experiment |
| dual MLP extended | 1200s | 1392 | 2.6908 | 1.5937 | 13,644,934 | extended experiment |
| architecture extended | 2000s | 1475 | 2.6636 | 1.5775 | 14,172,446 | extended experiment |
| exploratory long run | 9000s | 7007 | 2.4052 | 1.4245 | 16,121,692 | exploratory long run |

## Public Boundary

Unlike the Field Core and prediction branch, this case study may include code and metrics.

The results should always be labeled as Parameter-Golf-inspired experiments, not as official competition submissions.

## Reproducibility Note

The training script and run history are included as engineering artefacts. Individual runs may depend on external environment details such as available GPU hardware, dataset paths, tokenizer paths, environment variables, and wall-clock settings.
