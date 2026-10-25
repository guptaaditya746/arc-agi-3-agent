# Current blockers and risks

## Kaggle runtime / vLLM

- The public vLLM 0.23 wheelhouse contains CPython 3.12 wheels. The default Kaggle image used Python 3.13 and failed dependency resolution.
- Candidate v2 used the correct pinned Python 3.12 image but failed before execution: Kaggle could not mount the wheelhouse notebook source (`mbmmurad/vllm-0-23-0-tf5-wheelhouse`).
- Candidate metadata now uses the direct public dataset `ko0kip/vllm-0230-offline`, which the source notebook already searches as a wheelhouse path. Retry and confirm the source mounts.
- Candidate v3 skips duplicate model startup smoke on preview runs; actual competition reruns still launch vLLM through the agent.
- Kaggle previously rejected an additional RTX run because its batch GPU session limit was reached. Retry after a GPU slot is available.
- The competition rerun must start the local model, connect to `gateway:8001`, act on hidden games, and produce the gateway's real score artifact.

## Evaluation limits

- Only one competition submission remained available per day after the 0.15 baseline; the CLI then reported zero remaining. Avoid spending a new submission until the Gemma candidate has passed setup and preview validation.
- ARC-AGI-3 uses internet-disabled evaluation and has a nine-hour runtime cap. Hosted model APIs are out; the candidate uses an attached local model.
- The reported 0.86 belongs to another account's prior public run. It may not reproduce because versions, runtime images, and hidden games can differ.

## Security and licensing

- Do not commit Kaggle or GitHub access tokens. The tokens pasted in chat should be revoked and replaced.
- Keep third-party attribution for the Gemma candidate. The source notebook is Apache-2.0; Gemma model terms and attached vLLM package licenses remain separate.
