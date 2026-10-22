# REVERSE on Retinal Fundus Images

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/troy-choo/reverse-fundus/blob/main/notebooks/01_reverse_qwen_colab.ipynb)

Does a vision-language model's self-verification still work when the images are medical?

## Motivation

In medical imaging, a model that confidently describes a lesion that isn't there is a safety problem, not just an accuracy problem. [REVERSE](https://arxiv.org/abs/2504.13169) (Wu et al., NeurIPS 2025) trains a VLM to tag each key phrase as confident (`</CN>`) or unsure (`</UN>`), then backtracks and regenerates unsure phrases.

REVERSE was trained on natural images (COCO-style data). This project asks a simple question: **when the same model looks at retinal fundus photographs, do its `</UN>` flags line up with the lesions it gets wrong?**

## Setup

- Model: [`tsunghanwu/reverse_qwen25_vl`](https://huggingface.co/tsunghanwu/reverse_qwen25_vl) (Qwen2.5-VL-3B), compared with the base `Qwen/Qwen2.5-VL-3B-Instruct`
- Inference only, using the official [retrospective resampling code](https://github.com/tsunghan-wu/reverse_vlm); runs on a single Colab T4 GPU
- Data: public fundus images only (e.g. [APTOS 2019](https://www.kaggle.com/competitions/aptos2019-blindness-detection)), with diabetic retinopathy grades as ground truth

## Experiments

| # | Experiment | Status |
| --- | --- | --- |
| 1 | Reproduce REVERSE vs. base on natural images (COCO) | In progress |
| 2 | Phrase-level `P(</UN>)` on fundus images | Planned |
| 3 | Lesion hallucination rate on healthy (grade 0) images, base vs. REVERSE | Planned |
| 4 | Sensitivity to the `un_threshold` (0.003 / 0.01 / 0.03) | Planned |

## Results

_Coming soon._

## Repository layout

```
notebooks/   Colab notebooks, numbered in the order they were run
results/     CSV outputs and figures
```

## Acknowledgements

All model weights and the resampling code come from [REVERSE](https://github.com/tsunghan-wu/reverse_vlm) by Tsung-Han Wu, Heekyung Lee, Jiaxin Ge, Joseph E. Gonzalez, Trevor Darrell, and David M. Chan. This is an independent exploration and is not affiliated with the authors.
