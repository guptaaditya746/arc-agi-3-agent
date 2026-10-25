# ARC-AGI-3 agent improvement research

Checked 2026-10-25. This note compares the current systematic action sweep with public, runnable approaches and the competition's constraints. Public leaderboard scores are snapshots and may change.

## Practical findings

### 1. Replace blind cycling with observation-driven exploration

The current notebook cycles through six simple controls and a fixed 8×8 click grid. It does not use the frame to choose an action. A direct, low-dependency next step is a self-supervised action learner: encode the current 64×64, 16-color frame; track the action just taken; reward the action when it changes the board or advances `levels_completed`; then bias future choices toward actions that caused useful changes. Include an action/state novelty bonus so the policy keeps exploring when its last move had no effect. The public *Stochastic Goose* notebook implements a CNN over one-hot frames with five button logits and 4096 click logits, trains from observed frame-change rewards, and reports a public score of 0.25 with a 29-second T4×2 preview run. That is a concrete quick benchmark for moving beyond the current 0.15 submission, though its result is not a promise of improvement on our entry. [Notebook](https://www.kaggle.com/code/inversion/arc3-sample-submission-stochastic-goose)

### 2. For the largest likely gain, evaluate a local vision-language model

A public ARC-AGI-3 entry reports 0.86 on the public leaderboard using a locally served Gemma 4 31B vision-language model. It feeds recent frames in chronological order, requests structured JSON actions, validates/repairs outputs, and retains short reflection memory. This approach is much closer to the task's exploration, modeling, and planning goals than a button sweep. The notebook attaches the model and vLLM dependencies rather than calling a hosted API. [Notebook and score](https://www.kaggle.com/code/mbmmurad/arc-agi-3-lb-0-86-3rd-place-candidate-milestone/input?scriptVersionId=331511064), [author's description](https://www.kaggle.com/competitions/arc-prize-2026-arc-agi-3/discussion/716719)

This is the high-upside path, but it needs a compatible Kaggle model attachment, an offline inference stack, and the competition's upgraded accelerator. Reproduce locally on the public games first; do not assume the reported public score or model setup will reproduce without its exact inputs, code version, and runtime configuration.

### 3. Measure completion and action efficiency separately

ARC-AGI-3 evaluates multi-level games and rewards solving levels efficiently relative to human action counts. Log per game: levels completed, actions per level, resets, invalid actions, and frame-change rate. Compare action budgets and policies against the same public environments, then reserve the daily Kaggle submission for a measured candidate. A policy that explores more but spends many actions without progress may score worse. [Competition overview and code requirements](https://www.kaggle.com/competitions/arc-prize-2026-arc-agi-3), [ARC-AGI-3 goals](https://arcprize.org/arc-agi/3)

### 4. Keep the actual evaluation path intact

The official SDK provides `Arcade`/`EnvironmentWrapper`, action/observation types, and local versus competition modes. The bundled `ARC-AGI-3-Agents` project is MIT licensed. Use the competition's bundled wheels and environment files for offline development; competition evaluation has internet disabled, so hosted model APIs are out. Kaggle permits publicly available external data and pretrained models, but the notebook must finish within the listed nine-hour limit. [ARC toolkit](https://github.com/arcprize/arc-agi), [official agent framework and license](https://github.com/arcprize/ARC-AGI-3-Agents), [competition requirements](https://www.kaggle.com/competitions/arc-prize-2026-arc-agi-3)

## Recommended sequence

1. Add per-level logs and a consistent local score summary to the current public-game runner.
2. Implement the frame-change/reward learner from *Stochastic Goose* as a fast baseline, while retaining the sweep as a safe fallback. Check action masking and `ACTION6` coordinates against each frame's `available_actions`.
3. If available, reproduce the local Gemma 4 31B + vLLM notebook and its attached model/dependency inputs. Compare it with the learner on the same public environments and a runtime-matched action budget.
4. Make the final policy robust to malformed model output, empty frames, game resets, and timeouts; verify the notebook's offline run still emits `submission.parquet` before creating another competition submission.

## Licensing and submission notes

ARC Prize says prize-eligible participant-authored code/methods must be made public under a permissive public-domain-style license such as CC0 or MIT-0, and third-party code/methods must themselves allow open sharing. The ARC agent framework is MIT. The *Stochastic Goose* Kaggle notebook is marked Apache 2.0; if code is adapted, preserve its attribution/license notices and do not relabel copied third-party portions as MIT-0. The notebook itself and all added methods should remain public under a compatible license. [ARC Prize rules](https://arcprize.org/competitions/2026), [framework license](https://github.com/arcprize/ARC-AGI-3-Agents/blob/main/LICENSE), [Stochastic Goose notebook license](https://www.kaggle.com/code/inversion/arc3-sample-submission-stochastic-goose)
