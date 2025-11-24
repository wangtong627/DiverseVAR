# 🌟 DiverseVAR: Diversity Has Always Been There in Your Visual Autoregressive Models

## 💡 Introduction

We introduce **DiverseVAR**, a simple yet highly effective approach to restore the generative diversity of **Visual Autoregressive (VAR)** models **without any additional training**.

Despite their advantages in inference efficiency and image quality, VAR models frequently suffer from the well-known "diversity collapse," leading to a reduction in output variability, analogous to that observed in few-step distilled diffusion models. Through a thorough analysis of pre-trained VAR models, we found that:

* **Structure formation predominantly occurs in the early scales.**
* **Diversity is primarily governed by a "pivotal component" within these early scales.**

DiverseVAR leverages these findings by strategically intervening on the pivotal components during the inference process to unlock the inherent generative potential of VAR models.

## 🛠️ Method Overview

The DiverseVAR framework introduces two complementary, training-free sampling steps during inference, both focused on the manipulation of the pivotal components:

1.  **Soft-Suppression Regularization (SSR):**
    * Applied to the model's **input feature map**.
    * Mitigates diversity collapse by suppressing the pivotal components that control diversity formation.
    * In our implementation, SSR is realized through an exponential decay on the singular values of the input feature map.

2.  **Soft-Amplification Regularization (SAR):**
    * Applied to the model's **output feature map**.
    * Aims to further promote controlled diversity, ensuring that the enhanced variability maintains strong text-to-image alignment.
    * SAR is implemented by amplifying the singular values of the output features.

This framework successfully boosts generative diversity while maintaining high-fidelity synthesis and faithful semantic alignment.

## 🖼️ Qualitative Results

As shown below, our DiverseVAR (2nd and 4th rows) generates more diverse outputs compared to the vanilla VAR models (1st and 3rd rows), while preserving image-text consistency.

| **Prompt** | **"A man in a clown mask eating a donut"** | **"A cat wearing a Halloween costume"** | **"Golden Gate Bridge at sunset, glowing sky, ."** | **"A palace under the sunset"** |
| :---: | :---: | :---: | :---: | :---: |
| **Vanilla VAR (e.g., Infinity-2B)** |  |  |  |  |
| **DiverseVAR (Ours)** |  |  |  |  |
| **Prompt** | **"A cool astronaut floating in space"** | **"A cat riding a skateboard down a hill"** | | |
| **Vanilla VAR (e.g., Infinity-8B)** |  |  | | |
| **DiverseVAR (Ours)** |  |  | | |

## 📊 Quantitative Results (COCO Benchmarks)

The table below demonstrates that our DiverseVAR significantly improves diversity metrics (Recall, Cov. $\uparrow$, FID $\downarrow$) while maintaining comparable CLIPScore (CLIP $\uparrow$) on COCO2014-30K and COCO2017-5K benchmarks, compared to the original models.

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
