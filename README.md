<h1 align="center">
  <img src=".github/assets/logo.svg" width="72" alt="LongChang logo">
  <br>
  LongChang
</h1>

<p align="center">
  <strong><em>Can LLMs Uncover Hidden Physical Laws through Free Exploration?</em></strong>
</p>

<p align="center">
  <a href="https://zhenyangcs.github.io/LongChang-website/downloads/paper.pdf"><img src="https://img.shields.io/badge/Paper-PDF-4d7f9e?style=flat-square" alt="Read the paper"></a>
  <a href="https://zhenyangcs.github.io/LongChang-website/"><img src="https://img.shields.io/badge/Project-Page-315e68?style=flat-square" alt="Project page"></a>
  <a href="#citation"><img src="https://img.shields.io/badge/BibTeX-Cite-eaeaea?style=flat-square" alt="BibTeX citation"></a>
  <a href="https://zhenyangcs.github.io/LongChang-website/#worlds"><img src="https://img.shields.io/badge/Interactive_Demos-4d8569?style=flat-square" alt="Interactive demos"></a>
  <a href="#quick-start"><img src="https://img.shields.io/badge/Quick_Start-b08a45?style=flat-square" alt="Quick start"></a>
</p>

<p align="center">
  <a href="https://zhenyangcs.github.io/"><strong>Zhen&nbsp;Yang</strong></a><sup>1</sup> &nbsp;·&nbsp;
  <a href="https://encounter1997.github.io/"><strong>Wen&nbsp;Wang</strong></a><sup>3</sup> &nbsp;·&nbsp;
  <a href="https://xander23333.github.io/"><strong>Xander&nbsp;Xu</strong></a><sup>2*</sup> &nbsp;·&nbsp;
  <a href="https://www.yingcong.me/"><strong>Ying&#8209;Cong&nbsp;Chen</strong></a><sup>1,4*</sup>
  <br><br>
  <sup>1</sup>HKUST(GZ) &nbsp;·&nbsp; <sup>2</sup>Alibaba&nbsp;Group &nbsp;·&nbsp; <sup>3</sup>ZJU &nbsp;·&nbsp; <sup>4</sup>HKUST
  <br>
  <sub>* Co-corresponding authors</sub>
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

Requires **Python 3.12**.

```bash
git clone https://github.com/EnVision-Research/LongChang.git
cd LongChang

python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

### 2. Run

Set your OpenAI-compatible endpoint, API key, and model names:

```bash
export BASE_URL="https://your-api-endpoint.example/v1"
export API_KEY="your-api-key"
export MODEL="your-explorer-model"
export JUDGE_MODEL="your-judge-model"

python longchang/agent.py \
  --benchmark scenes/base_15.json \
  --scene 07_tile_restitution \
  --tell T0 --budget 20 \
  --output runs/first-exploration

python longchang/eval.py runs/first-exploration
```

`T0` enables free exploration; `--budget` limits interaction turns. These commands call your model API. Use a new output directory for each run.

Outputs: `session.json` (experiment record), `replay.bin` (replay), `eval.json` (assessment), and `run.log`.

<a id="citation"></a>

<h2 align="center">📚 Citation</h2>

```bibtex
@article{yang2026longchang,
  title={Can LLMs Uncover Hidden Physical Laws through Free Exploration?},
  author={Yang, Zhen and Wang, Wen and Xu, Xander and Chen, Ying-Cong},
  journal={arXiv preprint arXiv:xxx},
  year={2026}
}
```
