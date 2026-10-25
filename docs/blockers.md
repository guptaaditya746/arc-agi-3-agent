# Current blockers and risks

## Kaggle runtime / vLLM

- The public vLLM 0.23 wheelhouse contains CPython 3.12 wheels. The default Kaggle image used Python 3.13 and failed dependency resolution.
- Candidate v2 uses the same pinned Python 3.12 image as the public 0.86 source notebook, but its setup run remains `RUNNING`.
- Kaggle rejected another RTX run with `Maximum batch GPU session count of 2 reached`. Wait for a GPU slot and retry candidate v3, whose preview path avoids a separate model startup.
- The notebook preview is not the competition evaluation. The competition rerun must start the local model, connect to `gateway:8001`, act on the hidden games, and produce the gateway's real score artifact.

## Evaluation limits

- Only one competition submission remained available per day after the 0.15 baseline; the CLI then reported zero remaining. Avoid spending a new submission until the Gemma candidate has at least passed setup and preview validation.
- ARC-AGI-3 uses internet-disabled evaluation and has a nine-hour runtime cap. Hosted model APIs are out; the candidate uses an attached local model.
- The reported 0.86 belongs to another account's prior public run. It may not reproduce because versions, runtime images, and hidden games can differ.

## Security and licensing

- Do not commit Kaggle or GitHub access tokens. The tokens pasted in chat should be revoked and replaced.
- Keep third-party attribution for the Gemma candidate. The source notebook is Apache-2.0; Gemma model terms and attached vLLM package licenses remain separate.
