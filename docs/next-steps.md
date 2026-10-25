# Next steps

## Highest priority

1. Check `adi4r86/arc-agi-3-gemma-31b-agent` version 2. If it completes, inspect its logs and confirm the vLLM image-generation smoke passed.
2. When a GPU session is available, run candidate v3. It skips the duplicate preview startup smoke but keeps local vLLM startup in the competition execution path. Confirm the preview run produces `submission.parquet`.
3. After Kaggle's daily competition limit resets, submit the validated GPU notebook version. Record the submission reference, status, public score, and runtime here.

## Improve from measured results

4. Run the Gemma agent on a small representative public-game subset, then the full public set if runtime allows. Log levels completed, actions per level, resets, failed actions, and time per game.
5. Compare the same public games against the 0.15 baseline. Tune one variable at a time: frame context, reflection interval, action candidate count, and click-failure memory.
6. Use per-game scorecards to identify where the model stalls. Add targeted observation/action logic only when it improves held-out public games.
7. Keep the full candidate runtime under nine hours and preserve internet-disabled evaluation.

## Submission discipline

8. Reserve competition submissions for validated versions, since Kaggle showed zero daily submissions remaining after the first entry.
9. Keep each changed notebook public with its license/attribution and update this log with every score and failure.
