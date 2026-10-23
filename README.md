# 🪲 **Beetle Explorer**

Beetle Explorer lets you load and play with [Beetle](https://beetlelm.github.io) language models right in your browser—no coding required. It's the non-technical companion to the training framework: one Google Colab notebook where you pick a collection, language, curriculum, seed, and checkpoint from dropdown menus, move a few sliders, and generate text. If you want to *use* the models without writing any Python, start here.

> For a **detailed run-through**, check out the **full tutorial** on our website at [beetlelm.github.io/docs.html#beetle-explorer](https://beetlelm.github.io/docs.html#beetle-explorer).

---

## **Key Features**

1. **No-Code, Browser-Based Exploration**  
   - Everything happens in a single notebook: `notebooks/Beetle_Model_Explorer.ipynb`  
   - Open it in Colab, run the cells top to bottom, and interact through friendly widgets—no training stack, no setup

2. **Pick a Model from Plain-English Menus**  
   - Choose a **collection** (scale / training data), the **language(s)** it learned, the **curriculum** (how and when a second language was introduced), the **random seed**, and any extra settings  
   - The notebook reads the model's name and shows you a friendly summary of exactly what it is

3. **Travel Through Training with Checkpoints**  
   - Meet the model **fully trained** (`main`) or at an earlier **snapshot** (`step-N`) to watch how its behaviour changed as it learned  
   - Checkpoints are just Hugging Face revisions, so any point in training is one dropdown away

4. **Generate Text with Simple Sliders**  
   - Prompt the model with your own text and tune creativity, length, and more without touching code  
   - Optionally **look under the hood**: inspect the exact config, the training recipe, and the model's top next-word predictions

5. **Minimal Dependencies**  
   - Needs only `torch`, `transformers`, `huggingface_hub`, and `ipywidgets`—no training framework required  
   - Loading a checkpoint is a single `AutoModelForCausalLM.from_pretrained(repo, revision="step-N", trust_remote_code=True)` call

---

## **Quick Start**

1. **Open in Colab**

   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/beetlelm/beetle-explorer/blob/main/notebooks/Beetle_Model_Explorer.ipynb)

   Click the badge above (sign in to Google and authorise Colab's GitHub access the first time), then run the cells from top to bottom—each has a ▶️ play button.

   **Prefer to upload it yourself?** Download `notebooks/Beetle_Model_Explorer.ipynb`, go to [colab.research.google.com](https://colab.research.google.com), choose **File ▸ Upload notebook**, and pick the file.

2. **Pick a Model**

   Use the dropdowns to choose a **collection**, **language**, **curriculum**, **seed**, and **checkpoint**. The notebook summarises your choice in plain English and loads it under the hood with:

   ```python
   from transformers import AutoModelForCausalLM, AutoTokenizer

   repo = "Beetle-FineWeb-24B-4/beetle-monolingual-fineweb-24b-isl"
   model = AutoModelForCausalLM.from_pretrained(repo, revision="step-2048", trust_remote_code=True)
   tok   = AutoTokenizer.from_pretrained(repo, revision="step-2048", trust_remote_code=True)
   ```

3. **Generate Text**

   Type a prompt, move the sliders, and hit generate. These are small research models and will happily produce nonsense—that's part of what makes watching them learn interesting.

> 💡 **Running locally (optional):** Colab is the easy path, but you can run the notebook on your own machine too. Install the inference dependencies with `pip install -r requirements.txt`, then open `notebooks/Beetle_Model_Explorer.ipynb` in Jupyter.

---

## **Which collection to pick**

**New here?** Default to the full 24-billion-token release: **[Beetle-FineWeb-24B-4](https://huggingface.co/Beetle-FineWeb-24B-4)** and **[Beetle-FineWeb-24B-5](https://huggingface.co/Beetle-FineWeb-24B-5)**. Start with one of these.

For the full catalogue of collections, see **[beetlelm.github.io/models.html](https://beetlelm.github.io/models.html)**.

---

## **Part of the Beetle ecosystem**

- **[beetlelm](https://github.com/beetlelm/beetlelm)** 🚀 — core training framework (train your own Beetle models)
- **[beetle-data](https://github.com/beetlelm/beetle-data)** 📚 — bilingual data-preparation pipeline
- **[beetle-analyze](https://github.com/beetlelm/beetle-analyze)** 🔬 — evaluation and interpretability analysis toolkit
- **[beetle-explorer](https://github.com/beetlelm/beetle-explorer)** 🪲 *(this repo)* — no-code Colab model explorer

**Learn more:** project home at [beetlelm.github.io](https://beetlelm.github.io) · paper *Beetle: A Bilingual Model Suite for Modelling Second-Language Processing* (EMNLP 2026) at [arxiv.org/abs/2609.22633](https://arxiv.org/abs/2609.22633).

---

## **License**

Beetle Explorer is open-source under the [Apache License 2.0](LICENSE).
