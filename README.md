# 🪲 Beetle Explorer

**Load any Beetle language model, at any point in its training, and play with it — right in your browser, no coding required.**

This repository contains a single Google Colab notebook that lets anyone explore the [Beetle](https://huggingface.co/Beetle-HumanScale) family of small research language models. You pick the settings you care about, choose how far into training you want the model to be, and generate text with simple sliders.

It's built for people who want to *use* the models in applied settings — you do **not** need to know how to train models, or write any Python.

---

## ▶️ Open the notebook

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/suchirsalhan/beetle-explorer/blob/main/notebooks/Beetle_Model_Explorer.ipynb)

Click the badge above (you'll need to be signed in to Google, and — because this repo is private — authorise Colab's GitHub access the first time).

**No badge / prefer to upload it yourself?** Download `notebooks/Beetle_Model_Explorer.ipynb` from this repo, go to [colab.research.google.com](https://colab.research.google.com), choose **File ▸ Upload notebook**, and pick the file.

Then just run the cells from top to bottom (each has a ▶️ play button).

> 💡 For a free speed-up in Colab: **Runtime ▸ Change runtime type ▸ T4 GPU**. The models are small, so it also runs fine on CPU — just a little slower.

---

## What you can do

- **Choose a model** using plain-English menus:
  - which **collection** (scale / training data) it comes from,
  - the **language(s)** it learned,
  - the **teaching strategy** (how and when a second language was introduced),
  - the **random seed** and any **extra settings** (anti-forgetting, per-language vocabulary, and so on).
  The notebook reads the model's name and shows you a friendly summary of exactly what it is.
- **Choose a checkpoint** — meet the model when it's *fully trained* (`main`) or at an earlier **snapshot** (`step-…`) to see how its behaviour changed as it learned.
- **Generate text** from your own prompts, with sliders for creativity, length, and more.
- **Look under the hood** (optional): see the exact configuration, the training recipe, and the model's top next-word predictions.

## The five Beetle collections

| Collection | What it is |
|---|---|
| [Beetle-HumanScale](https://huggingface.co/Beetle-HumanScale) | Trained on roughly the amount of language a child hears. |
| [Beetle-FineWeb-100M](https://huggingface.co/Beetle-FineWeb-100M) | Small models trained on 100M tokens of the multilingual FineWeb-2 web corpus. |
| [Beetle-FineWeb-2B](https://huggingface.co/Beetle-FineWeb-2B) | Trained on 2B tokens of FineWeb-2. |
| [Beetle-FineWeb2-24B](https://huggingface.co/Beetle-FineWeb2-24B) | Larger-data models trained on 24B tokens of FineWeb-2. |
| [Beetle-FineWeb](https://huggingface.co/Beetle-FineWeb) | The original FineWeb (24B-token) collection. |

## Running locally (optional)

You don't need to — Colab is the easy path — but if you'd rather run it on your own machine:

```bash
pip install -r requirements.txt
jupyter notebook notebooks/Beetle_Model_Explorer.ipynb
```

---

## About the models

Beetle models are small research language models for studying **learning dynamics** and **bilingual language acquisition**. Each was checkpointed densely through training so you can inspect *how* — not just *whether* — it learned. They are small and will happily produce nonsense; that's part of what makes watching them learn interesting.

Under the hood, loading a Beetle checkpoint is just:

```python
from transformers import AutoModelForCausalLM, AutoTokenizer
repo = "Beetle-FineWeb-100M/beetle-monolingual-fineweb-100m-isl"
model = AutoModelForCausalLM.from_pretrained(repo, revision="step-2048", trust_remote_code=True)
tok   = AutoTokenizer.from_pretrained(repo, revision="step-2048", trust_remote_code=True)
```

The notebook wraps this (plus a couple of Beetle-specific fixes for generation) in a friendly interface.

**Want to train your own Beetle models?** See the [beetlelm](https://github.com/suchirsalhan/beetlelm) training framework — that's the technical, research-facing project this notebook complements.

## Licence

Apache-2.0. See [LICENSE](LICENSE).
