<div align="center">
<h1> 🌟 DiverseVAR </h1>
<h3>Diversity Has Always Been There in Your Visual Autoregressive Models</h3>

[Tong Wang](https://wangtong627.github.io/)<sup>1,2</sup>, [Guanyu Yang](https://cs.seu.edu.cn/gyyang/main.htm)<sup>1</sup>, [Nian Liu](https://sites.google.com/site/liunian228/)<sup>2</sup>, [Kai Wang](https://wangkai930418.github.io/)<sup>3</sup>, [Yaxing Wang](https://yaxingwang.github.io/)<sup>4</sup>, [Abdelrahman M Shaker](https://amshaker.github.io/)<sup>2</sup>,
<br>
[Salman Khan](https://salman-h-khan.github.io/)<sup>2</sup>, [Fahad Shahbaz Khan](https://sites.google.com/view/fahadkhans/home)<sup>2</sup>, [Senmao Li](https://sen-mao.github.io/)<sup>4,2</sup>

<sup>1</sup> Southeast University, <sup>2</sup> MBZUAI, <sup>3</sup> City University of Hong Kong, <sup>4</sup> Nankai University

[![arXiv](https://img.shields.io/badge/arXiv-2511.17074-red)](https://arxiv.org/abs/2511.17074)
[![Website](https://img.shields.io/badge/Project-Website-87CEEB)](https://wangtong627.github.io/DiverseVAR)
</div>

<p align="center">
    <img src="https://i.imgur.com/waxVImv.png" alt="DiverseVAR">
</p>

## 💡 Introduction

We introduce **DiverseVAR**, a simple yet highly effective approach to restore the **generative diversity** of **Visual Autoregressive (VAR)** models **without any additional training**.

Despite their advantages in inference efficiency and image quality, VAR models frequently suffer from the well-known "**diversity collapse**," leading to a reduction in output variability, analogous to that observed in few-step distilled diffusion models. Through a thorough analysis of pre-trained VAR models, we found that:

* **Structure formation predominantly occurs in the early scales**.
* **Diversity is primarily governed by a "pivotal component" within these early scales**.

DiverseVAR leverages these findings by strategically intervening on the pivotal components during the inference process to unlock the inherent generative potential of VAR models.



## 🛠️ Method Overview

The DiverseVAR framework introduces two complementary, training-free regularization steps during inference, both focusing on the manipulation of the pivotal components:

1.  **Soft-Suppression Regularization (SSR):**
    * Applied to the model's **input feature map ($\tilde{F}_{k-1}$)** at early scales.
    * Mitigates diversity collapse by suppressing the dominant singular values (our proxy for the pivotal component).

2.  **Soft-Amplification Regularization (SAR):**
    * Applied to the model's **output feature map ($\hat{F}_{k}^{o}$)**.
    * Aims to further promote controlled diversity and improve image-text alignment, especially for numerical attributes.

This training-free framework effectively boosts generative diversity while maintaining high-fidelity synthesis and faithful semantic alignment.



## 🖼️ Qualitative Results

The figure below illustrates the enhanced generative diversity achieved by our DiverseVAR (2nd and 4th rows) compared to the vanilla VAR models (1st and 3rd rows). Our method produces a wider variety of realistic images while preserving high-quality and strong text-image alignment.

<div align="center">
    <img src="DiverseVAR.png" alt="DiverseVAR Qualitative Results">
    <br>
    Figure 1. Multiple generation samples from the vanilla VAR models (1st and 3rd rows) and our DiverseVAR (2nd and 4th rows).
</div>

The text prompts used are: "A man in a clown mask eating a donut", "A cat wearing a Halloween costume", "Golden Gate Bridge at sunset, glowing sky, .", "A palace under the sunset", "A cool astronaut floating in space", and "A cat riding a skateboard down a hill".



## 📊 Quantitative Results (COCO Benchmarks)

The table below demonstrates that our DiverseVAR significantly improves diversity metrics ($\text{Recall} \uparrow$, $\text{Cov.} \uparrow$, $\text{FID} \downarrow$) while maintaining comparable $\text{CLIPScore} (\text{CLIP} \uparrow)$ on the COCO2014-30K and COCO2017-5K benchmarks.

| Dataset | Method | Recall $\uparrow$ | Cov. $\uparrow$ | FID $\downarrow$ | CLIP $\uparrow$ |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **COCO2014-30K** | Infinity-2B | 0.316 | 0.651 | 28.48 | 0.313 |
| | **+Ours (DiverseVAR)** | **0.385** | **0.690** | **22.96** | 0.313 |
| | Infinity-8B | 0.451 | 0.740 | 18.79 | 0.319 |
| | **+Ours (DiverseVAR)** | **0.497** | **0.748** | **14.26** | 0.315 |
| **COCO2017-5K** | Infinity-2B | 0.408 | 0.832 | 39.01 | 0.313 |
| | **+Ours (DiverseVAR)** | **0.480** | **0.860** | **33.39** | 0.313 |
| | Infinity-8B | 0.563 | 0.892 | 29.47 | 0.319 |
| | **+Ours (DiverseVAR)** | **0.585** | 0.892 | **25.01** | 0.316 |

* $\uparrow$: Higher is better. $\downarrow$: Lower is better.



## 📄 Citation

Please cite our paper if you find this work useful for your research:

```bibtex
@article{wang2025diversity,
  title={Diversity Has Always Been There in Your Visual Autoregressive Models},
  author={Wang, Tong and Yang, Guanyu and Liu, Nian and Wang, Kai and Wang, Yaxing and Shaker, Abdelrahman M and Khan, Salman and Khan, Fahad Shahbaz and Li, Senmao},
  journal={arXiv preprint arXiv:2511.17074},
  year={2025}
}
