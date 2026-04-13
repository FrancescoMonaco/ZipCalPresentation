---
theme: default
css: styles.css
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
What is Model Compression?

Model compression is the process of reducing the size and computational requirements of a machine learning model while maintaining its performance. 

This is often achieved through techniques that remove unnecessary parameters, reduce the precision of weights or distill knowledge from a larger model into a smaller one.

---
transition: fade
---

# The Setting: What is Pruning?

<div style="font-size: 1.1rem; max-width: 600px; margin: 0 auto 1rem auto;">
Pruning removes unnecessary weights or neurons from a neural network, making it smaller and faster while aiming to keep accuracy high.
</div>
<PruningAnimation />

---
transition: fade
---

# The Setting: What is Quantization?

<div style="font-size: 1.1rem; max-width: 600px; margin: 0 auto 1rem auto;">
Quantization reduces the precision of the numbers used to represent weights and activations, making the model smaller and faster, often with little loss in accuracy.
</div>
<QuantizationAnimation />

---
transition: fade
---

# The Setting: Calibration Data for Model Compression
Desired Properties
<br><br>
1. **Scalability (G1):** Can handle very large datasets with minimal computation.
<br>
2. **Model-agnostic (G2):** Finds the most informative examples without needing to run the full model.
<br>
3. **Inter-domain generalization (G3):** Works for both single-domain and multi-domain datasets by design.

---
transition: fade
---
# The Setting: Existing Methods
<br>

Many studies have shown that the choice of calibration data significantly impacts the performance of compressed models. Analysing the impact of length, domain, and diversity of calibration data on the performance of compressed models.

Despite this information the most common method to select calibration data is still random sampling!

SoTA techniques work by selecting samples that minimize model's perplexity, which requires running the full model on the entire dataset.

---
transition: fade
---


# The Model: Zipfian Sampling

<ZipfianAnimation />

<div style="font-size: 1.1rem; max-width: 600px; margin: 1.5rem auto 0 auto; text-align: center;">
In natural language, a few words (like "the", "of", "and") are extremely common, while most words are rare. This pattern given by the frequency of words is called a <strong>Zipfian distribution</strong>. We want to leverage this property to select <em>calibration data that closely represents the distribution of tokens in the original dataset</em>.
</div>


---
transition: fade
---

# The Model: Zipfian Sampling
Introducing ZipCal


ZipCal is a method that samples data based on the frequency of tokens, following a Zipfian distribution.


The data used for calibration is sampled according to the frequency of tokens, with more frequent tokens being more likely to be included in the calibration set.

Samples are chosen as $s^*\leftarrow \argmax_{s\in D} |V_s\setminus V_{covered}|$

---
transition: fade
---

# Experiments: Scalability
Time to select the calibration samples for different methods.

<img src="/images/scalability_all.png" alt="Scalability Results" style="width: 100%; max-width: 600px; margin: 1.5rem auto; display: block;" />  

---
transition: fade
---

# Experiments: Quality
Mean accuracy across 11 different tasks and 18 different calibration datasets.

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

*full results include 2 other compression techniques

---
transition: fade
---

# On The Difficulty of Choosing Calibration Data
 <br>

From the full results an interesting pattern emerges: the best calibration data for a certain task is not the one from the same domain. And no correlation emerges between the best calibration data and the task domain.

E.g., **General Knowledge** tasks perform better under models compressed using data from the **Math** domain!

This behaviour is exhacerbated when we consider multi-lingual setting, where we find that **the best calibration data for a given language is not necessarily in that language**.



---
transition: fade
---

# Obtaining Property G3: Multi-Domain ZipCal
<br>
Aggregating multiple datasets and running ZipCal would insert a bias towards bigger datasets.

<br><br>
We run ZipCal on each dataset **separately** and then aggregate the results using a **k-centers clustering** algorithm to select the most representative samples across all datasets.