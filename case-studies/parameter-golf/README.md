# Parameter-Golf-inspired GPT Training

## Summary

This case study documents an experimental GPT training project inspired by the OpenAI Parameter Golf challenge format.

It is **not an official competition submission** and is not presented as a leaderboard result.

The project started as a real attempt to participate in the challenge. Over time, it shifted into a research and engineering log because the explored architecture direction no longer fit cleanly inside the strict competition constraint envelope.

The main focus was not only to train a smaller GPT model.

The experiment explored whether a compact model could produce more useful learning movement per step by expanding and structuring its internal representation space.

The main architecture directions were:

```text
dual-space MLP
→ token-local reaction signals
→ attention enrichment
→ low-tension descriptor overlays
→ base/refine dual pass
→ refine-to-base backbinding
→ cross-stage bridge
```

The project did not produce a valid leaderboard entry.

Its public value is the documented development path: what was tried, what was observed, which ideas produced signals, which ideas were too expensive, and why the competition track was eventually abandoned.

## Current Status

This case study is best described as:

```text
completed experimental log / public evidence block
```

The experiment is not presented as a production model, a validated architecture, or an official competition result.

The final state can be summarized as:

```text
challenge-inspired GPT training experiment
→ multiple architecture modifications tested
→ run metrics collected
→ strong internal signals observed
→ runtime / constraint mismatch confirmed
→ no official submission
→ public documentation preserved
```

Unlike the Field Core and related private system descriptions, this case study may include code, run history, metrics, and experiment notes.

## Selected Run Evidence

The following selected runs are engineering logs, not official competition records.

| Run label | Wall-clock setting | Steps reached | Validation loss | BPB | int8+zlib bytes | Status |
|---|---:|---:|---:|---:|---:|---|
| baseline local | 600s | 863 | 2.8101 | 1.6643 | 11,817,558 | constraint-close experiment |
| dual MLP extended | 1200s | 1392 | 2.6908 | 1.5937 | 13,644,934 | extended experiment |
| architecture extended | 2000s | 1475 | 2.6636 | 1.5775 | 14,172,446 | extended experiment |
| exploratory long run | 9000s | 7007 | 2.4052 | 1.4245 | 16,121,692 | exploratory long run |

These values show that the project reached functioning training runs and measurable improvements across experimental settings.

They should not be interpreted as leaderboard-compliant results.

## Early Dual-Space Observation Evidence

One important early diagnostic comparison tested the model with and without active negative-space usage.

The setup compared:

```text
neg_beta = 0.0
→ baseline-like run without active negative-space usage

neg_beta = 1.0
→ dual-space run with active negative-space usage
```

The short-run result did not show an immediate final BPB win for the active negative-space variant.

However, the internal observations were important.

Without active negative-space usage, the negative side showed strong drift and asymmetry. With active negative-space usage, the positive and negative sides stayed much more balanced.

This did not prove that dual-space improved the final metric.

It did show that the additional space was not simply dead or meaningless. It produced measurable internal behavior and became the basis for later token-local signals.

The conservative interpretation was:

```text
dual-space dynamics were measurable
but not automatically converted into better final BPB
```

## Development History

## Phase 1 — Competition Goal and Early Learning Phase

The project began as a real attempt to participate in the OpenAI Parameter Golf challenge.

The original goal was competitive: build a small GPT-style model that could satisfy the challenge constraints and produce a valid entry.

The early phase was also a learning phase.

At the beginning of the competition, the internal structure of LLMs, the details of GPT architectures, and the mathematical background of transformer training were still being learned during the experiment itself.

Because of that, the first idea was intentionally simple:

```text
Can the usable internal representation space of a small GPT be expanded
without violating the hard competition constraints?
```

The first runs were therefore observation runs.

They were not designed to prove a final architecture theory. They were used to inspect whether an additional internal direction could be introduced and whether the model would show measurable structure, drift, collapse, or stable behavior.

## Phase 2 — Dual-Space MLP

The first concrete model change happened in the MLP block.

The idea was to split the internal activation behavior into a positive and a negative side.

At a high level:

```text
activation
→ positive space
→ negative space
→ delta between both spaces
```

The motivation was to increase the usable internal representation space under the hard challenge constraints.

This was not meant as a large architectural system at first. It began as a direct test of whether the model could make use of an additional internal direction.

The early observation runs suggested that the model could absorb this expanded space.

The negative side did not simply collapse into irrelevant noise. It showed measurable dynamics, including drift and balance behavior depending on whether the negative space was actively used.

This led to the next question:

```text
If the expanded space changes internal dynamics,
why does it not directly translate into better final metrics?
```

This became the first major translation bottleneck of the project.

## Phase 3 — Tau as a Learnable Token-Local Reaction Signal

The next idea came directly from the measurable relation between positive and negative activation space.

The dual-space MLP did not only add another internal direction. It also created a new measurable difference signal.

```text
positive space
negative space
delta between both
```

This made it possible to derive token-local tension values.

Tau emerged from this idea.

At this stage, Tau was still close to the MLP block. It was not a large separate architecture module. The idea was to use the positive/negative delta to generate local reaction values for each token.

The intended logic was:

```text
positive / negative activation split
→ delta between both spaces
→ token-local tension strength
→ Tau / Alpha / Base-Keep reaction values
→ gated carry signal
→ modified MLP output
```

This allowed the model to react differently depending on how strong the positive/negative tension was for a token.

Tau was not only a fixed diagnostic value. In the experimental implementation, the reaction values were initialized conservatively but built as learnable mappings from token-local tension. This allowed the model to learn how strongly it should react to the measured dual-space tension during training.

In the development history, this was an important shift:

```text
from expanded space as extra capacity
to expanded space as a source of learnable internal reaction signals
```

The surrounding transformer architecture had not yet been redesigned around Tau. But Tau already represented the first attempt to turn observed dual-space behavior into an active internal mechanism.

## Phase 4 — High-Tau Attention Energy

After Tau and token-local reaction values were introduced, the next bottleneck became model-wide usage.

The model now had a way to measure local tension between positive and negative activation space. However, this signal still lived close to the MLP path.

The first attention idea was simple:

```text
tokens with higher internal tension
→ should receive more internal attention energy
```

The reasoning was that a token with high positive/negative tension might be more uncertain, more ambiguous, or harder to assign.

If that was true, the model might benefit from treating those tokens with more internal focus inside attention.

The first attention experiments were therefore not a complete redesign of attention.

They were an attempt to let token-local tension influence how strongly a token was handled.

The development logic was:

```text
dual-space MLP
→ measurable token tension
→ Tau / reaction values
→ high-tension tokens
→ increased attention priority or energy
```

The observed effect was small or not clearly visible.

This led to a counter-hypothesis.

## Phase 5 — Low-Tau Anchor Hypothesis

The weak effect of the high-tension attention idea raised a new question:

```text
What if the most useful tokens are not the uncertain ones,
but the stable ones?
```

Low-Tau tokens could represent parts of the sequence that were easier to assign, easier to learn, or more internally stable.

Instead of spending extra attention energy on uncertain tokens, the model might benefit from building stable internal reference points from tokens it already handled more confidently.

The new question became:

```text
Can low-tension tokens act as anchors for more stable internal connections?
```

This shifted the interpretation of Tau.

Tau was no longer only a possible uncertainty signal. It also became a possible way to identify stable regions in the token stream.

The development logic became:

```text
dual-space MLP
→ token-local tension signal
→ high-tension attention idea
→ weak observed effect
→ low-tension anchor hypothesis
```

This was an important conceptual shift.

The experiment moved from trying to spend more energy on uncertain tokens toward trying to build more stable structure around tokens that the model seemed to handle more confidently.

## Phase 6 — Low-Tau Descriptor Overlay

The low-Tau anchor hypothesis led to the low-Tau descriptor overlay.

At a high level, the idea was:

```text
low-tension token signal
→ soft descriptor space
→ role-like gate
→ key/value overlay in attention
→ more stable token-to-token structure
```

The descriptor was not intended as a fixed symbolic role.

It was a small learnable coordinate system that could attach additional structure to low-tension tokens.

This represented another shift in the experiment:

```text
from spending extra attention on uncertain tokens
to building stable internal anchors from confident tokens
```

After this direction was introduced, small improvements became visible in some runs.

However, the signal was still mixed and partly oscillating. The metrics did not stabilize enough to make a strong claim that the mechanism was clearly solved.

The conservative interpretation was:

```text
low-Tau descriptor overlays showed possible value
but not enough stable evidence for a clear conclusion
```

In later versions, this direction also opened the path toward descriptor diagnostics and structure-cluster observations.

Those should be understood as exploratory tools for observing whether the low-Tau descriptor space formed reusable internal patterns, not as validated final mechanisms.

## Phase 7 — Direct Intervention Attempts

After the low-Tau descriptor overlay, the experiment showed small but unclear improvements.

This created the next question:

```text
Is the model failing to fully absorb the new internal signal?
```

Several direct intervention attempts were tested.

These included attempts to make the internal signal more visible to the training process, including more direct interaction with the learned update path or loss-related behavior.

The purpose was to test whether the useful internal signal existed but was not entering the optimization process strongly enough.

These directions did not produce a clear result.

They were therefore not treated as the main path forward.

The lesson from this phase was:

```text
a visible internal signal is not enough
and forcing it more directly into training does not automatically make it useful
```

## Phase 8 — Base/Refine Dual Pass

After the direct intervention attempts did not produce a clear conclusion, the next major architecture step was the base/refine dual pass.

This was not introduced as a generic second pass.

It had a specific structural purpose.

At this stage, the model had started to build a loop between MLP-side dual-space signals and attention-side enrichment. The concern was that this loop could become an open drift point.

If the model continuously transforms its own internally generated signal without a stable reference, the signal may become harder to interpret and less clearly tied to the original training objective.

The base pass was introduced as an anchor.

The intended separation was:

```text
base pass
→ prepare and cache a stable local reference state

refine pass
→ use that anchored state for the actual trainable transfer
```

In the training loop, the base pass prepared the internal anchor state first. The refine pass then performed the actual loss-producing step and backpropagation.

The public idea can be summarized as:

```text
input batch
→ base pass creates internal anchors
→ refine pass uses anchors for controlled transfer
→ refine loss drives the update
```

This allowed the model to use the attention-enriched and dual-space-derived reactions without relying on a single open self-referential path.

In the development history, this was a major shift:

```text
dual-space MLP
→ token-local Tau signals
→ attention enrichment
→ low-Tau descriptor anchors
→ risk of open drift
→ base pass as anchor
→ refine pass as controlled continuation
```

This direction produced the first clearer improvements in the metrics.

The additional computation increased per-step time, but that cost was accepted. The goal at this stage was no longer to keep the architecture minimal at all costs. The goal was to test whether the anchored dual-pass structure could produce more useful learning movement, even if each step became slower.

After this point, the dual-pass structure remained part of the architecture.

Later tweaks focused on clarifying which parts of the internal signal should become part of the learned update path and which parts should remain as anchor or reference information.

The central distinction became:

```text
what should be learned from
vs.
what should remain available as a stable anchor
```

## Phase 9 — Refine-to-Base Backbinding

After the base/refine dual pass was established, the model showed stronger internal movement and clearer metric improvements.

However, later training still showed drift-like behavior.

The refine path appeared capable of producing strong movement, but part of that movement seemed to come from the model's own internal dynamics rather than from a sufficiently stable reference.

This created a generalization concern:

```text
strong refine movement
→ possible short-term specialization
→ later drift
→ weak long-term generalization
```

The next idea was to bind the refine movement back to the base movement.

The goal was not to prevent specialization completely. Specialization was allowed, and even desired, as long as it stayed connected to the anchored base state.

The intended logic became:

```text
base movement
→ stable reference direction

refine movement
→ stronger specialized adjustment

refine-to-base backbinding
→ each specialized movement keeps a reference connection
```

This was introduced to reduce the risk that the refine path would become too self-referential.

The broader idea was:

```text
the model may specialize,
but each refinement should remain tied to an anchored base signal
```

This direction only partially addressed the drift problem.

Because the backbinding itself was still created inside the refine path, the refine path could partly absorb the backbinding mechanism into its own specialization behavior.

This led to the final major architecture direction of the experiment.

## Phase 10 — Cross-Stage Bridge Between Base, Attention, and Refine

The next idea was to create a bridge between the three main internal stages:

```text
MLP base
↔ attention
↔ MLP refine
```

The motivation was that these stages did not appear to grow information density at the same speed.

Attention, in particular, could create a much richer internal information width after a certain point in training. The refine path then had to process this enriched state, but it did not necessarily have the same contextual width available.

This created a possible drift source:

```text
attention builds richer context
→ refine receives a compressed or mismatched continuation
→ refine specializes from an incomplete view
→ later training drift becomes more likely
```

The bridge idea attempted to reduce this mismatch.

Instead of only connecting refine back to base, the goal was to let base, attention, and refine share enough structural information that each stage could track the movement of the others.

The intended logic became:

```text
base movement
→ attention enrichment
→ refine movement

bridge across all three
→ each stage can observe the broader movement
→ specialization remains more traceable
→ drift risk is reduced
```

The strongest version of this idea used a second Q/K/V-style attention computation to carry an additional vector across the full hidden space.

This vector was initialized from the base side and allowed the later stages to keep a broader reference to the original anchored movement.

One run with this stronger bridge direction showed very strong results.

However, the cost was too high.

The doubled attention-style computation quickly increased step time so much that the approach became impractical under the challenge-style runtime constraints.

Because of that, the full version was discarded and reduced into the compromise architecture used in the later experimental state.

The lesson from this phase was:

```text
the bridge direction looked promising,
but the strongest implementation was too expensive
```

The final architecture therefore kept the idea of cross-stage communication, but not the full double-attention version.

## Phase 11 — RunPod H100 Test and End of Competition Track

After the compromise architecture was reached, the final practical test was run on a single H100 RunPod server.

The purpose was to see whether the stronger architecture could still be made practical under a more capable GPU setup.

This test did not produce a new architecture direction.

Instead, it clarified the main practical limitation.

The model contained many small local computations. Even on the H100 setup, the full batch-size target became difficult to handle efficiently.

The issue was not simply raw GPU power, but the mismatch between the architecture's many local operations and the challenge-style runtime constraints.

At this point, it became clear that the experiment could no longer realistically satisfy the competition constraints well enough for an official entry.

The competition track was therefore abandoned.

The project shifted into documentation mode:

```text
competition attempt
→ architecture exploration
→ H100 practicality check
→ constraint mismatch confirmed
→ no official submission
→ public experiment log
```

The final result should therefore be understood as a Parameter-Golf-inspired research and engineering case study, not as a leaderboard submission.

## Key Learnings

## 1. Internal Signals Are Not Automatically Metric Improvements

The dual-space MLP created measurable internal behavior.

The negative space was not simply unused noise, and the positive/negative relation became useful enough to derive token-local signals.

However, this internal structure did not automatically become a better final BPB.

The project repeatedly showed a gap between:

```text
visible internal structure
and
stable external metric improvement
```

This became one of the central findings.

## 2. Stable Tokens May Matter as Much as Difficult Tokens

The first instinct was to give high-tension tokens more attention energy.

That effect was weak.

The later low-Tau anchor hypothesis suggested that stable, easier-to-assign tokens may provide better internal reference points than uncertain tokens.

This became one of the more useful conceptual pivots of the experiment.

## 3. Stronger Architecture Can Lose to Runtime Constraints

Several architecture directions became more interesting as systems ideas than as competition solutions.

The base/refine dual pass and cross-stage bridge improved the structural logic of the model, but they also introduced more local computation.

Under hard wall-clock and batch-size constraints, that matters heavily.

A model can do more useful work per step and still become impractical if each step becomes too expensive.

## 4. Generalization Drift Was the Hardest Problem

The later architecture states could create stronger internal movement.

The difficult part was keeping that movement tied to stable reference structure over time.

This created the final sequence of ideas:

```text
base anchor
→ refine movement
→ refine-to-base backbinding
→ cross-stage bridge
```

The experiment did not fully solve this problem.

It clarified why the problem mattered.

## Limitations

This case study has several important limitations.

It did not achieve leaderboard competitiveness.

It was not submitted as an official competition entry.

Some experiments relaxed or exceeded the strictest challenge-style conditions in order to explore architecture behavior.

Several promising ideas increased step time too much for the competition setting.

The observed runs depend on environment details such as GPU availability, wall-clock budget, dataset paths, tokenizer paths, environment variables, compression behavior, and training configuration.

The run history should therefore be interpreted as an engineering log, not as a clean benchmark suite.

## Included Files

The public artefacts for this case study are:

- [`train_gpt_runpod.py`](./train_gpt_runpod.py) — main experimental training script
- [`run_history.csv`](./run_history.csv) — raw logged runs and metrics
- [`README.md`](./README.md) — experiment summary and interpretation

The earlier baseline-compatible script may also be referenced as:

```text
train_gpt.py
```

The `train_gpt_runpod.py` file should be treated as the main script for this experiment log.

## Public Boundary

Unlike the Field Core and prediction branch, this case study may include code and metrics.

The results should always be labeled as:

```text
Parameter-Golf-inspired experiments
not official competition submissions
not leaderboard results
```

The public repository may include:

- training script
- run history
- selected metrics
- experiment notes
- implementation discussion

But it should not overstate the results.

The goal is to document what was tried, what happened, what failed, and what was learned.

## Reproducibility Note

The training script and run history are included as engineering artefacts.

Individual runs may depend on external environment details such as:

- GPU hardware
- runtime limit
- Python environment
- dependency versions
- dataset path
- tokenizer path
- environment variables
- compression settings

Reproducing the exact values may require matching the original environment.

## Disclaimer

This is not an official competitive submission.

It is an independent experimental documentation case study intended for open discussion, research transparency, and engineering reference.
