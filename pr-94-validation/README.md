# PR 94 validation artifacts

This folder contains the modded-nanoGPT validation artifacts for the AdamW
fallback LM-head learning-rate scale comparison discussed in microsoft/dion#94.

Setup:

- Base code: `kellerjordan/modded-nanogpt` commit `c26c2a1`
  (`new optimizer`, Oct 4 2024), the minimal Muon-introduction version.
- Change for this experiment: replace local Muon with local `DionSimple`, using
  AdamW fallback for the tied `lm_head` / embedding weight.
- Hardware: 4x B200 per run.
- Data: FineWeb GPT-2 token shards from `kjj0/fineweb10B-gpt2`.
- Training: 500 steps, validation every 50 steps, same seed/settings for both
  runs except AdamW fallback head scale.

Runs. Logs are trimmed to begin at the first training step:

- `dion_correct_500_slurm-117993.out`: AdamW fallback head scale `1.0`
- `dion_incorrect_500_slurm-117994.out`: AdamW fallback head scale
  `1 / sqrt(768)`
