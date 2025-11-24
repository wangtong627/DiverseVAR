<div align="center">
<h1> 🌟 DiverseVAR </h1>
<h2>Diversity Has Always Been There in Your Visual Autoregressive Models</h2>

[Tong Wang](https://wangtong627.github.io/)<sup>1,2</sup>, [Guanyu Yang](https://cs.seu.edu.cn/gyyang/main.htm)<sup>1,\*</sup>, Nian Liu<sup>2,\*</sup>, Kai Wang<sup>2</sup>, Yaxing Wang<sup>2</sup>, Abdelrahman M Shaker<sup>2</sup>, Salman Khan<sup>2</sup>, [Fahad Shahbaz Khan](https://sites.google.com/view/fahadkhans/home)<sup>2</sup>, Senmao Li<sup>2</sup>

<sup>1</sup> Southeast University, <sup>2</sup> Mohamed Bin Zayed University of Artificial Intelligence

<small><span style="color:#E63946; font-weight:bold;">\*</span> indicates corresponding authors</small>

<br>

[![License](https://img.shields.io/badge/License-CC_BY--NC--SA_4.0-lightgrey)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![arXiv](https://img.shields.io/badge/arXiv-2511.17074-red)](https://arxiv.org/abs/2511.17074)

</div>

***

## ⚠️ Code and Model Availability

**This work is currently under confidential review for CVPR 2026 Submission #2086.**

**For this reason, the code and pre-trained models are temporarily unavailable and cannot be made public at this time.** We are committed to releasing the code immediately upon paper acceptance. Thank you for your patience and understanding!

***

## 💡 Introduction

We introduce **DiverseVAR**, a simple yet highly effective approach to restore the generative diversity of **Visual Autoregressive (VAR)** models **without any additional training**.

[cite_start]Despite their advantages in inference efficiency and image quality, VAR models frequently suffer from the well-known "**diversity collapse**," leading to a reduction in output variability, analogous to that observed in few-step distilled diffusion models[cite: 27]. Through a thorough analysis of pre-trained VAR models, we found that:

* [cite_start]**Structure formation predominantly occurs in the early scales**[cite: 108, 109].
* [cite_start]**Diversity is primarily governed by a "pivotal component" within these early scales**[cite: 120, 463].

[cite_start]DiverseVAR leverages these findings by strategically intervening on the pivotal components during the inference process to unlock the inherent generative potential of VAR models[cite: 466].

***

## 🛠️ Method Overview

The DiverseVAR framework introduces two complementary, training-free regularization steps during inference, both focusing on the manipulation of the pivotal components:

1.  **Soft-Suppression Regularization (SSR):**
    * Applied to the model's **input feature map ($\tilde{F}_{k-1}$)** at early scales.
    * [cite_start]Mitigates diversity collapse by suppressing the dominant singular values (our proxy for the pivotal component)[cite: 485].

2.  **Soft-Amplification Regularization (SAR):**
    * Applied to the model's **output feature map ($\hat{F}_{k}^{o}$)**.
    * [cite_start]Aims to further promote controlled diversity and improve image-text alignment, especially for numerical attributes[cite: 633, 637].

[cite_start]This training-free framework effectively boosts generative diversity while maintaining high-fidelity synthesis and faithful semantic alignment[cite: 117].

***

## 🖼️ Qualitative Results

The figure below illustrates the enhanced generative diversity achieved by our DiverseVAR (2nd and 4th rows) compared to the vanilla VAR models (1st and 3rd rows). Our method produces a wider variety of realistic images while preserving high-quality and strong text-image alignment.



<div align="center">
    <img src="figure1_main_samples_compressed.pdf" alt="DiverseVAR Qualitative Results">
    <br>
    [cite_start]Figure 1. Multiple generation samples from the vanilla VAR models (1st and 3rd rows) and our DiverseVAR (2nd and 4th rows)[cite: 22].
</div>

[cite_start]The text prompts used are: "A man in a clown mask eating a donut", "A cat wearing a Halloween costume", "Golden Gate Bridge at sunset, glowing sky, .", "A palace under the sunset", "A cool astronaut floating in space", and "A cat riding a skateboard down a hill"[cite: 24].

***

## 📊 Quantitative Results (COCO Benchmarks)

The table below demonstrates that our DiverseVAR significantly improves diversity metrics ($\text{Recall} \uparrow$, $\text{Cov.} \uparrow$, $\text{FID} \downarrow$) while maintaining comparable $\text{CLIPScore} (\text{CLIP} \uparrow)$ on the COCO2014-30K and COCO2017-5K benchmarks.

| Dataset | Method | Recall $\uparrow$ | Cov. $\uparrow$ | FID $\downarrow$ | CLIP $\uparrow$ |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **COCO2014-30K** | Infinity-2B | 0.316 | 0.651 | 28.48 | [cite_start]0.313 [cite: 687] |
| | **+Ours (DiverseVAR)** | **0.385** | **0.690** | **22.96** | [cite_start]0.313 [cite: 687] |
| | Infinity-8B | 0.451 | 0.740 | 18.79 | [cite_start]0.319 [cite: 687] |
| | **+Ours (DiverseVAR)** | **0.497** | **0.748** | **14.26** | [cite_start]0.315 [cite: 687] |
| **COCO2017-5K** | Infinity-2B | 0.408 | 0.832 | 39.01 | [cite_start]0.313 [cite: 687] |
| | **+Ours (DiverseVAR)** | **0.480** | **0.860** | **33.39** | [cite_start]0.313 [cite: 687] |
| | Infinity-8B | 0.563 | 0.892 | 29.47 | [cite_start]0.319 [cite: 687] |
| | **+Ours (DiverseVAR)** | **0.585** | 0.892 | **25.01** | [cite_start]0.316 [cite: 687] |

* $\uparrow$: Higher is better. $\downarrow$: Lower is better.

***

## 📄 Citation

Please cite our paper if you find this work useful for your research:

```bibtex
@misc{wang2025diversityvisualautoregressivemodels,
      title={Diversity Has Always Been There in Your Visual Autoregressive Models}, 
      author={Tong Wang and Guanyu Yang and Nian Liu and Kai Wang and Yaxing Wang and Abdelrahman M Shaker and Salman Khan and Fahad Shahbaz Khan and Senmao Li},
      year={2025},
      eprint={2511.17074},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={[https://arxiv.org/abs/2511.17074](https://arxiv.org/abs/2511.17074)}, 
}
