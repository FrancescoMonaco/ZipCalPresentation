---
theme: default
#css: styles.css
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: '#e7f0f9'
# some information about your slides (markdown enabled)
title: Frequency Matters
titleTemplate: '%s'
author: 'Francesco Pio Monaco'
info: |
  Paper Presentation
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
# seoMeta:
#  ogImage: https://cover.sli.dev
---

# <span class="zipcal-title">FRREQUENCCY<br>MA<span style="font-variant-ligatures: none; font-feature-settings: 'liga' 0, 'dlig' 0, 'calt' 0;">TT</span>ERSS</span>

Fast Model-Agnostic Data Curation for Pruning and Quantization

<div class="absolute bottom-20">
  <span class="font-700">
    Francesco Pio Monaco, Elia Cunegatti, Flavio Vella, Giovanni Iacca  -  April 2026
  </span>
</div>

---
transition: fade
---

# The Setting: Model Compression
What is model compression?

<br>
*Model compression* reduces model size and computational cost while preserving performance.
<br>
<br>
It is typically achieved through pruning, quantization, or distillation.

---
transition: fade
---

# The Setting: What is Pruning?

<div style="font-size: 1.5rem; max-width: 600px; margin: 0 auto 1rem auto;">
<strong>Pruning</strong> removes unnecessary weights or neurons from a neural network, even entire blocks (e.g. attention heads).
</div>
<PruningAnimation />

---
transition: fade
---

# The Setting: What is Quantization?

<div style="font-size: 1.5rem; max-width: 600px; margin: 0 auto 1rem auto;">
<strong>Quantization</strong> reduces the precision of the numbers used to represent weights and activations.
</div>
<QuantizationAnimation />

---
transition: fade
---

# The Setting: Why Calibration Data Matters

<br>
To run a compression framework, we need examples to capture the model's activation statistics: this subset is called *calibration data*.


---
transition: fade
---

# The Setting: Calibration Data for Model Compression
Desired properties
<br><br>
1. **Scalability (G1):** Handle very large datasets with minimal computation.
<br>
2. **Model-agnostic (G2):** Find informative examples without running the full model.
<br>
3. **Inter-domain generalization (G3):** Work by design for both single-domain and multi-domain data.

---
transition: fade
---

# The Setting: Existing Methods
<br>

Many studies show that calibration data selection strongly affects compressed-model quality, especially across length, domain, and diversity choices. [Bandari et al, 2024](https://scholar.google.com/scholar_url?url=https://aclanthology.org/2024.emnlp-main.1004/&hl=it&sa=T&oi=gsr-r&ct=res&cd=0&d=9018053943015335144&ei=yfDdaaroJfLLieoP_67FyQQ&scisig=ADi0EEU6d0-OeMrv1jyabpKFLxe1) [Oh and Oh, 2025](https://scholar.google.com/scholar_url?url=https://aclanthology.org/anthology-files/anthology-files/pdf/findings/2025.findings-emnlp.1054.pdf&hl=it&sa=T&oi=gsr-r-ggp&ct=res&cd=0&d=14192841322382081900&ei=ufDdaY7zMqztieoPm_X9-Aw&scisig=ADi0EEVkxgdprPmvqy4u8LCPuhAL)

Despite this, random sampling is still widely used in practice.

Most state-of-the-art methods minimize model perplexity, which requires full-model inference over the entire dataset.

---
transition: fade
---

# The Setting: Existing Methods
State-of-the-art approaches

<br>
They optimize perplexity-based objectives (plus additional terms), but this requires full-model inference on all candidate samples, making the process computationally expensive and poorly scalable.


---
transition: fade
---


# The Model: Zipfian Sampling

<ZipfianAnimation />

<div style="font-size: 1.1rem; max-width: 600px; margin: 1.5rem auto 0 auto; text-align: center;">
In natural language, a few words (like "the", "of", "and") are extremely common, while most words are rare. This frequency pattern is called a <strong>Zipfian distribution</strong>. We leverage it to select <em>calibration data that better matches the token distribution of the original dataset</em>.
</div>


---
transition: fade
---

# The Model: Zipfian Sampling
Introducing ZipCal

<br>
ZipCal samples data according to token frequency, following a Zipfian distribution.
<br>
More frequent tokens are more likely to appear in the calibration set, but we also cover the tail of the distribution.
<br>
Samples are chosen as $s^*\leftarrow \argmax_{s\in D} |V_s\setminus V_{covered}|$
<br>
At each step, we pick the sample that contributes the largest set of not-yet-covered tokens.

---
transition: fade
---

# Experiments: Token Distribution
Token distribution of the original dataset (grey) and calibration sets of 16 random (blue), COLA (green) and ZipCal (red) samples.

<img src="/images/gsm8k_winogrande_hellaswag_token_dist_16samples-1.png" alt="Token Distribution" style="width: 200%; max-width: 930px; margin: 4rem -1.5rem; display: block;" />  

---
transition: fade
---

# Experiments: Scalability
Calibration sample selection time across methods.

<img src="/images/scalability_all.png" alt="Scalability Results" style="width: 100%; max-width: 600px; margin: 1.5rem auto; display: block;" />  

---
transition: fade
---

# Experiments: Quality
Mean accuracy across 11 tasks and 18 calibration datasets.

<table style="width: 100%; border-collapse: collapse; table-layout: fixed; font-size: 0.84rem; line-height: 1.28;">
  <thead>
    <tr>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>Method</strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>Model</strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>Dense</strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>COLA</strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>ZipCal</strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>Delta</strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>Speedup</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2" style="padding: 6px 8px; border: 1px solid #cbd5e1; font-weight: 700; vertical-align: middle; background-color: #f8fafc;">Wanda 25%</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">Llama-3.1-8B-Instruct</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">63.36</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">62.47</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">62.94</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #dcfce7; color: #166534; font-weight: 700;">+0.47</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #f7fcdc; color: #5f5708; font-weight: 700;">228x</td>
    </tr>
    <tr>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">gemma-2-9B-Instruct</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">61.11</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">61.15</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">61.57</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #dcfce7; color: #166534; font-weight: 700;">+0.42</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #f7fcdc; color: #5f5708; font-weight: 700;">260x</td>
    </tr>
    <tr>
      <td rowspan="2" style="padding: 6px 8px; border: 1px solid #cbd5e1; font-weight: 700; vertical-align: middle; background-color: #f8fafc;">GPTQ W4A16</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">Llama-3.1-8B-Instruct</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 63.36 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 61.02 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 60.89 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #fef3c7; color: #92400e; font-weight: 700;"> -0.13 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #f7fcdc; color: #5f5708; font-weight: 700;"> 228x </td>
    </tr>
    <tr>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">gemma-2-9B-Instruct</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 61.11 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 60.56 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 61.41 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #dcfce7; color: #166534; font-weight: 700;"> +0.85 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #f7fcdc; color: #5f5708; font-weight: 700;"> 260x </td>
    </tr>
  </tbody>
</table>

*Full results include two additional compression techniques.

---
transition: fade
---

# On The Difficulty of Choosing Calibration Data
 <br>

From the full results, a clear pattern emerges: the best calibration data for a task often does not come from the same domain.

For example, **General Knowledge** tasks can perform better when models are compressed with **Math** calibration data.

This behavior is exacerbated in multilingual settings, where **the best calibration data for a given language is not necessarily in that language**.



---
transition: fade
---

# Obtaining Property G3: Multi-Domain ZipCal
<br>
If we aggregate multiple datasets and run ZipCal once, selection becomes biased toward larger datasets.

<br>
<br>
To avoid this, we run ZipCal on each dataset **separately**, then merge candidates with **k-centers clustering** to select representative samples across all datasets.

---
transition: fade
---

# Experiments: Quality
Mean accuracy across 11 tasks and 18 calibration datasets.

<table style="width: 100%; border-collapse: collapse; table-layout: fixed; font-size: 0.84rem; line-height: 1.28;">
  <thead>
    <tr>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>Method</strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>Model</strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>Dense</strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>COLA</strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>ZipCal Multi-Domain </strong></th>
      <th style="padding: 6px 8px; border: 1px solid #cbd5e1;"><strong>Delta</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2" style="padding: 6px 8px; border: 1px solid #cbd5e1; font-weight: 700; vertical-align: middle; background-color: #f8fafc;">Wanda 25%</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">Llama-3.1-8B-Instruct</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">63.36</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">62.47</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">64.48</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #dcfce7; color: #166534; font-weight: 700;">+2.01</td>
    </tr>
    <tr>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">gemma-2-9B-Instruct</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">61.11</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">61.15</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">61.98</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #dcfce7; color: #166534; font-weight: 700;">+0.83</td>
    </tr>
    <tr>
      <td rowspan="2" style="padding: 6px 8px; border: 1px solid #cbd5e1; font-weight: 700; vertical-align: middle; background-color: #f8fafc;">GPTQ W4A16</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">Llama-3.1-8B-Instruct</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 63.36 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 61.02 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 61.48 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #dcfce7; color: #166534; font-weight: 700;"> +0.46 </td>
    </tr>
    <tr>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;">gemma-2-9B-Instruct</td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 61.11 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 60.56 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1;"> 61.54 </td>
      <td style="padding: 6px 8px; border: 1px solid #cbd5e1; background-color: #dcfce7; color: #166534; font-weight: 700;"> +0.98 </td>
    </tr>
  </tbody>
</table>

*Full results include two additional compression techniques.


---
transition: fade
---

# Main Takeaways 
<br>

- Choosing calibration data is hard.
- Compressing models using multi-domain data can lead to better performances across tasks.
- ZipCal is a simple, model-agnostic method to select calibration data that matches the token distribution of the original dataset.
- ZipCal naturally extends to multi-domain settings, where it can select representative samples across datasets, leading to better performance than single-domain selection.