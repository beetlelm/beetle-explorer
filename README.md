# 🪲 Beetle Explorer

**Load any Beetle language model, at any point in its training, and play with it — right in your browser, no coding required.**

This repository contains a single Google Colab notebook that lets anyone explore the [Beetle](https://huggingface.co/Beetle-HumanScale) family of small research language models. You pick the settings you care about, choose how far into training you want the model to be, and generate text with simple sliders.

It's built for people who want to *use* the models in applied settings — you do **not** need to know how to train models, or write any Python.

---

## ▶️ Open the notebook

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/beetlelm/beetle-explorer/blob/main/notebooks/Beetle_Model_Explorer.ipynb)

Click the badge above (you'll need to be signed in to Google, and authorise Colab's GitHub access the first time).

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

## Which collection should I use?

> ⚠️ **Start with the final 24-billion-token release.** Because of a token-budget
> drift bug, several earlier collections never reached their advertised size (see
> the note below). For new work, default to **Beetle-FineWeb-24B-4** or
> **Beetle-FineWeb-24B-5** — these are the only genuine 24B-token collections.

| Collection | What it is |
|---|---|
| [Beetle-FineWeb-24B-4](https://huggingface.co/Beetle-FineWeb-24B-4) | **Recommended.** A genuine 24B-token FineWeb-2 collection (final release). |
| [Beetle-FineWeb-24B-5](https://huggingface.co/Beetle-FineWeb-24B-5) | **Recommended.** A genuine 24B-token FineWeb-2 collection (final release). |
| [Beetle-HumanScale](https://huggingface.co/Beetle-HumanScale) | Trained on roughly the amount of language a child hears. |
| [Beetle-FineWeb-100M](https://huggingface.co/Beetle-FineWeb-100M) | Small models trained on 100M tokens of the multilingual FineWeb-2 web corpus. |

### A note on the earlier "24B" and "2B" collections

A token-budget drift bug meant several earlier collections stopped well short of
their nominal token counts. They remain available for reference, but their names
overstate how much data they actually saw:

| Collection | Advertised | Actually reached |
|---|---|---|
| [Beetle-FineWeb2-24B](https://huggingface.co/Beetle-FineWeb2-24B) | 24B tokens | ~3B tokens |
| [Beetle-FineWeb3-24B](https://huggingface.co/Beetle-FineWeb3-24B) | 24B tokens | ~3B tokens |
| [Beetle-FineWeb-2B](https://huggingface.co/Beetle-FineWeb-2B) | 2B tokens | ~300M tokens |

For a full explanation of the token-budget bug and how the final `-24B-4` /
`-24B-5` collections were produced, see
**[beetlelm.github.io/models.html](https://beetlelm.github.io/models.html)**.
New users should default to the `-24B-4` / `-24B-5` collections above.

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
repo = "Beetle-FineWeb-24B-4/beetle-monolingual-fineweb-24b-isl"
model = AutoModelForCausalLM.from_pretrained(repo, revision="step-2048", trust_remote_code=True)
tok   = AutoTokenizer.from_pretrained(repo, revision="step-2048", trust_remote_code=True)
```

The notebook wraps this (plus a couple of Beetle-specific fixes for generation) in a friendly interface.

## Learn more

- **Tutorial:** [beetle-explorer walkthrough](https://beetlelm.github.io/docs.html#beetle-explorer) on the project docs.
- **Models & Data (collection guide):** https://beetlelm.github.io/models.html
- **Project home:** https://beetlelm.github.io
- **Framework overview:** https://beetlelm.github.io/framework.html
- **Paper:** *Beetle: A Bilingual Model Suite for Modelling Second-Language Processing* (EMNLP 2026) — https://arxiv.org/abs/2609.22633

## Part of the Beetle ecosystem

- **[beetlelm](https://github.com/beetlelm/beetlelm)** — core training framework (train your own Beetle models).
- **[beetle-data](https://github.com/beetlelm/beetle-data)** — bilingual data-preparation pipeline.
- **[beetle-analyze](https://github.com/beetlelm/beetle-analyze)** — evaluation and interpretability analysis toolkit.
- **[beetle-explorer](https://github.com/beetlelm/beetle-explorer)** (this repo) — no-code Colab model explorer.

## Licence

Apache-2.0. See [LICENSE](LICENSE).
