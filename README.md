# ARC-AGI-3 agent work

Workspace for participating in the [ARC Prize 2026 ARC-AGI-3 Kaggle competition](https://www.kaggle.com/competitions/arc-prize-2026-arc-agi-3). It records the submitted baseline, the stronger Gemma 4 candidate, observed issues, and the next experiments.

## Current status — 2026-10-25

- Kaggle account is entered in the competition.
- Baseline submission **57631315** completed with public score **0.15**.
- The baseline policy cycles through simple controls and click points. It is useful as a working reference but does not reason over observations.
- A separate Gemma 4 31B candidate is based on MB Boktiar Mahbub Murad's public Apache-2.0 notebook, which reported **0.86** on the public leaderboard. That is a prior result, not a guaranteed score for this account.
- Candidate v2 is still marked running on Kaggle. Candidate v3 has been saved without running and disables the duplicate model startup smoke on preview runs. No new competition submission has been made.

See [progress](docs/progress.md), [blockers](docs/blockers.md), [next steps](docs/next-steps.md), and the [research summary](docs/research-strategy.md).

## Contents

- [`notebooks/baseline/`](notebooks/baseline/): the original 0.15 entry and its Kaggle metadata.
- [`notebooks/gemma31b/`](notebooks/gemma31b/): attributed, public Gemma 4 31B candidate with offline vLLM setup.
- [`docs/`](docs/): status, blockers, experiment plan, and source-backed research notes.

The competition entry requires internet-disabled Kaggle notebook runs, a `submission.parquet` preview artifact, and a maximum nine-hour runtime. The Gemma model and vLLM wheelhouse are attached by Kaggle metadata; large model/data files are intentionally not stored in this repository.
