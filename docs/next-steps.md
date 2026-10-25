# Next steps

## Highest priority

1. Push the Gemma candidate with `ko0kip/vllm-0230-offline` attached directly as a dataset source. Confirm the input mounts and the pinned Python 3.12 environment installs vLLM.
2. Once a GPU session is available, run the preview version. It should skip duplicate model startup and still emit `submission.parquet`.
3. After Kaggle's daily competition limit resets, submit the validated GPU notebook version. Record the submission reference, status, public score, and runtime here.

## Improve from measured results

4. Run the Gemma agent on a small representative public-game subset, then the full public set if runtime allows. Log levels completed, actions per level, resets, failed actions, and time per game.
5. Compare the same public games against the 0.15 baseline. Tune one variable at a time: frame context, reflection interval, action candidate count, and click-failure memory.
6. Use per-game scorecards to identify where the model stalls. Add targeted observation/action logic only when it improves held-out public games.
7. Keep the full candidate runtime under nine hours and preserve internet-disabled evaluation.

## Submission discipline

8. Reserve competition submissions for validated versions, since Kaggle showed zero daily submissions remaining after the first entry.
9. Keep each changed notebook public with its license/attribution and update this log with every score and failure.
