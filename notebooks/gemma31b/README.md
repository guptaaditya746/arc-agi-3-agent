# Gemma 4 31B ARC-AGI-3 candidate

This candidate adapts a public Apache-2.0 Kaggle notebook by MB Boktiar Mahbub Murad, linked and attributed in the notebook and `THIRD_PARTY_NOTICES.md` in the GitHub repository. The source notebook reported 0.86 on the public leaderboard; that score may not reproduce here.

The candidate attaches the public Gemma 4 31B model and the public offline vLLM wheelhouse dataset, runs with internet disabled, and pins the Python 3.12 Kaggle image required by those wheels. The previous v2 run failed because Kaggle could not mount the wheelhouse as a notebook source; metadata now uses the direct dataset source instead.
