<h1 align="center">
  <img src=".github/assets/logo.svg" width="72" alt="LongChang logo">
  <br>
  LongChang
</h1>

<p align="center">
  <strong><em>Can LLMs Uncover Hidden Physical Laws through Free Exploration?</em></strong>
</p>

<p align="center">
  <a href="https://arxiv.org/abs/2610.37649">
    <img src="https://img.shields.io/badge/Paper-arXiv-b31b1b?style=flat-square" alt="Paper"></a>
  <a href="https://zhenyangcs.github.io/LongChang-website/">
    <img src="https://img.shields.io/badge/Project-Page-2f9e6e?style=flat-square" alt="Project Page"></a>
  <a href="#citation">
    <img src="https://img.shields.io/badge/BibTeX-Cite-eaeaea?style=flat-square" alt="BibTeX"></a>
  <br>
  <a>
    <img src=".github/assets/project-page-note.svg" width="520" alt="All interactive demos and detailed experimental results are on the project page.">
  </a>
</p>

<br>

<p align="center">
  <a href="https://zhenyangcs.github.io/"><strong>Zhen&nbsp;Yang</strong></a><sup>1</sup> &nbsp;·&nbsp;
  <a href="https://encounter1997.github.io/"><strong>Wen&nbsp;Wang</strong></a><sup>3</sup> &nbsp;·&nbsp;
  <a href="https://xander23333.github.io/"><strong>Xander&nbsp;Xu</strong></a><sup>2*</sup> &nbsp;·&nbsp;
  <a href="https://www.yingcong.me/"><strong>Ying&#8209;Cong&nbsp;Chen</strong></a><sup>1,4*</sup>
</p>

<p align="center">
  <sup>1</sup>&nbsp;HKUST(GZ) &nbsp;·&nbsp; <sup>2</sup>&nbsp;Alibaba&nbsp;Group &nbsp;·&nbsp; <sup>3</sup>&nbsp;ZJU &nbsp;·&nbsp; <sup>4</sup>&nbsp;HKUST
</p>

<p align="center">
  <sub><sup>*</sup> Co-corresponding authors</sub>
</p>

<p align="center">
  <a href="https://zhenyangcs.github.io/LongChang-website/#worlds">
    <img src=".github/assets/world.webp" width="480" alt="A LongChang world with balls, a pendulum, and a balance.">
  </a>
</p>

<h2 align="center">🧭 Overview</h2>

**LongChang** lets LLMs explore MuJoCo worlds with altered physical laws, choose their own questions, and build instruments to test explanations. The framework automates scene construction, exploration, evaluation, and scene evolution. Discoveries must be correct and supported by the explorer's experiments.

<a id="quick-start"></a>

<h2 align="center">⚡ Quick Start</h2>

### 1. Install

Requires **Python 3.12** and the full LongChang codebase (`requirements.txt` and `longchang/`), which is not currently included in this repository.

```bash
git clone https://github.com/EnVision-Research/LongChang.git
cd LongChang

python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

### 2. Run

Run from the repository root. Set your OpenAI-compatible endpoint, API key, and model names:

```bash
export BASE_URL="https://your-api-endpoint.example/v1"
export API_KEY="your-api-key"
export MODEL="your-explorer-model"
export JUDGE_MODEL="your-judge-model"
```

#### Run all 15 scenes

The `models` command uses `longchang/scenes/base_15.json` and includes all 15 scenes by default, unless `SCENES` is set to a subset. The following configuration uses free exploration (`T0`), a budget of 100 interaction turns, and 3 repeats per scene:

```bash
export MODELS="$MODEL" SCENES=""
export TELLS=T0 BUDGET=100 REPEATS=3 CONCURRENCY=2

# Preview the full run plan without calling model APIs.
DRY_RUN=1 OUT_ROOT=runs/benchmark \
  python longchang/run.py models

# Run the full benchmark and automatically evaluate each run.
DRY_RUN=0 ALLOW_PAID_API=1 OUT_ROOT=runs/benchmark \
  python longchang/run.py models
```

This schedules **45 runs** (15 scenes × 3 repeats), with up to 2 runs in parallel. Evaluation uses `JUDGE_MODEL`; no separate `eval.py` command is needed for batch runs. The preview does not create the output directory. Use a new `OUT_ROOT` for each actual execution.

Per-run results are saved under `runs/benchmark/<scene-id>/<model>/r<repeat>/T0/`. The output root also contains `plan.json`, `summary.json`, an aggregate `eval.json`, and `run_errors.json`.

Without the explicit overrides above, the batch defaults are `TELLS=T1`, `BUDGET=20`, `REPEATS=1`, and `CONCURRENCY=2`. Batch mode reads explorer models from `MODELS`, while single-scene mode uses `MODEL`.

#### Try a single scene

```bash
python longchang/agent.py \
  --benchmark longchang/scenes/base_15.json \
  --scene 07_tile_restitution \
  --tell T0 --budget 20 \
  --output runs/first-exploration

python longchang/eval.py runs/first-exploration
```

This example uses a smaller budget of 20 interaction turns. Exploration and evaluation call your model API. Use a new output directory for each run.

Outputs: `session.json` (experiment record), `replay.bin` (replay), `eval.json` (assessment), and `run.log`.

<a id="citation"></a>

<h2 align="center">📚 Citation</h2>

```bibtex
@article{yang2026longchang,
  title={Can LLMs Uncover Hidden Physical Laws through Free Exploration?},
  author={Yang, Zhen and Wang, Wen and Xu, Xander and Chen, Ying-Cong},
  journal={arXiv preprint arXiv:2610.37649},
  year={2026}
}
```
