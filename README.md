# adaption-autoscientist-challenge-50000-prize-pool-xenova
Hackathon team repository for Xenova - [hackindia-team:adaption-autoscientist-challenge-50000-prize-pool:xenova]

# MedLlama-India-70B

> Fine-tuned Llama 3.3 70B for Indian Medical Entrance  
> Examinations (NEET-PG & AIIMS-PG)  
> Adaption Labs AutoScientist Challenge 2026 — Healthcare Category

---

## Overview

MedLlama-India-70B is a 70B-parameter Llama 3.3 model fine-tuned specifically for **Indian postgraduate medical entrance exams** (NEET‑PG, AIIMS‑PG/INI‑CET). It is optimized not just to pick the right option, but to **explain clinical reasoning the way Indian examiners test it** — including why each distractor is wrong in a given vignette.

The model, dataset, and demo are released as open source so that **any Indian medical student, college, NGO, or state programme can build on top of them**, without paywalls or per‑query API lock‑in.

---

## Problem

Postgraduate medical entrance in India is brutally competitive and structurally unequal:

- **High competition, limited seats**  
  Around **2.3 lakh MBBS graduates appear for NEET‑PG each year**, competing for roughly **70,000–73,000 postgraduate seats (MD/MS/DNB/PG Diploma)**.[web:116][web:130][web:134][web:14]  
  Most candidates will not get their desired branch or college, even if they qualify.

- **Coaching is expensive and geographically concentrated**  
  Offline NEET‑PG coaching in metros like Delhi, Mumbai and Hyderabad often costs **₹1–2 lakh per year**, once you include tuition, tests and support.[web:55][web:56][web:60]  
  Even “affordable” online PG platforms typically charge **₹20,000–40,000+ per year** for serious prep plans, which is still steep for many interns and bonded doctors.[web:47][web:52][web:58]

- **Most AI is trained for USMLE, not NEET‑PG**  
  Existing open medical LLMs (Meditron‑70B, Me‑LLaMA‑70B, OpenMedLLM‑70B, OpenBioLLM‑70B, etc.) are trained mostly on **global biomedical literature and USMLE‑style benchmarks**.[web:21][web:23][web:25][web:92]  
  They are not tuned to the **Indian MBBS curriculum, Indian epidemiology, drug brands, or national programmes** that dominate NEET‑PG and AIIMS‑PG questions.[web:89][web:95][web:96][web:112]

- **Reasoning style mismatch**  
  NEET‑PG / AIIMS‑PG questions are full of **plausible distractors** that may be medically correct in some context but wrong for the exact vignette, stage, or national guideline used in the question.[web:91][web:95][web:96]  
  Most LLMs are trained to output the right option, not to **teach the decision boundary** between options the way good faculty do.

**Goal:** Build an open, India‑localized 70B model that can act like a **24×7 reasoning tutor** for NEET‑PG/AIIMS‑PG — especially for students who cannot afford metro‑city coaching.

---

## Solution

MedLlama-India-70B is designed as a **domain‑specialized, India‑aware 70B LLM** for postgraduate medical entrance, with three pillars:

### 1. India-first medical knowledge

We fine‑tune on Indian exam–style MCQs and vignettes so the model “thinks” in the same universe as actual NEET‑PG/AIIMS‑PG papers:

- **MedMCQA core**  
  We use the **MedMCQA dataset** — ~**194,000 multiple-choice questions** curated from Indian medical entrance exams, covering **21 subjects and ~2,400 topics** across pre‑clinical, para‑clinical, and clinical disciplines.[web:89][web:88][web:121]

- **Curriculum and guideline alignment**  
  Questions are aligned with the **Indian MBBS curriculum and NEET‑PG syllabus**, including standard texts (Gray’s, Robbins, Goodman & Gilman, Harrison’s, Dutta’s Obstetrics) and Indian public‑health content.[web:95][web:96][web:97]

- **Epidemiology and programme context**  
  We emphasize Indian epidemiology (e.g., TB as India’s leading infectious killer) and national programmes such as **NTEP/RNTCP, NVBDCP, NHM**, so the model internalizes the **same public‑health framing** that exam setters use.[web:101][web:103][web:108][web:110][web:112][web:115]

### 2. Distractor-aware clinical reasoning

Instead of just learning “question → right option”, MedLlama-India-70B is fine‑tuned on **full reasoning traces**:

- Step‑by‑step explanation for the **correct answer**  
- Explicit explanations of **why each incorrect option is wrong in this vignette** (e.g., outdated regimen, wrong line of treatment, contraindicated for this comorbidity, not the next best investigation)

This training style mirrors how top NEET‑PG faculty teach: they don’t just give answers; they **teach elimination logic and context boundaries**, which makes knowledge robust to rephrasing and new variants.[web:92][web:94]

### 3. Open, composable infrastructure

- Built on a **Llama 3.3 70B base model** so that the community can reuse existing tooling and optimizations.  
- Released under an **open license**, making it possible for:
  - State governments to deploy “AI resident tutor” services for medical colleges  
  - NGOs to build free doubt‑solving bots for rural doctors  
  - Startups and coaching institutes to add their own UX, analytics, and RAG layers on top

---

## Results

### Automatic evaluation (internal)

We evaluate on a held‑out subset of Indian exam–style MCQs with both **medical** and **general** reasoning components.

| Metric            | Base | Fine-tuned | Improvement |
|-------------------|------|-----------:|------------:|
| Medical Win Rate  | 26%  | 74%        | +185%       |
| Overall Win Rate  | 20%  | 80%        | +300%       |
| Dataset Grade     | B    | A          | ↑           |
| Dataset Percentile| 28.9 | 57.7       | +28.8 pts   |

> These are internal evaluation metrics on our curated Indian exam benchmark. They are reported here to show relative improvement, not to claim SOTA across all medical LLMs.

### External baseline

As a reference point, published work reports around **44.7% accuracy on MedMCQA** for a Mistral‑7B–based model (BioMistral‑7B), which we treat as a strong open‑source baseline for Indian medical MCQs.[web:94][web:131]

---

## Links

| Resource        | URL |
|----------------|-----|
| 🤗 Model        | [xenkrypt/MedLlama-India-70B](https://huggingface.co/xenkrypt/MedLlama-India-70B) |
| 📊 Dataset (HF) | [xenkrypt/MedLlama-India-Dataset](https://huggingface.co/datasets/xenkrypt/MedLlama-India-Dataset) |
| 📦 Dataset (Kaggle) | [tharunkrishnath/medllama-india-dataset](https://www.kaggle.com/datasets/tharunkrishnath/medllama-india-dataset) |
| 🚀 Demo         | [MedLlama-India-Demo](https://huggingface.co/spaces/xenkrypt/MedLlama-India-Demo) |

---

## Responsible Use

MedLlama-India-70B is a **study aid**, not a replacement for formal medical training or clinical judgment. Outputs can be wrong or outdated. For clinical decisions, always defer to:

- Latest national and institutional guidelines  
- Senior faculty and clinicians  
- Official NMC/NBEMS notifications

---

## Citation

If you use MedLlama-India-70B or the MedLlama-India dataset in research or products, please cite the dataset and this repository (citation block to be added once a preprint is available).
