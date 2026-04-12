---
# You can also start simply with 'default'
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
<style>
@font-face {
  font-family: 'Stretch';
  src: url('./fonts/StretchPro.otf') format('opentype');
  font-display: swap;
}

.zipcal-title {
  font-family: 'Stretch', sans-serif;
  font-size: 3rem;
  letter-spacing: 0.05em;
  font-variant-ligatures: discretionary-ligatures contextual;
  font-feature-settings: "liga" 1, "dlig" 1, "calt" 1;
}
</style>



# <span class="zipcal-title">FRREQUENCCY<br>MAT‌TERSS</span>

Fast Model-Agnostic Data Curation for Pruning and Quantization

<div class="absolute bottom-10">
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

1. **Scalability (G1):** Can handle very large datasets with minimal computation.
2. **Model-agnostic (G2):** Finds the most informative examples without needing to run the full model.
3. **Inter-domain generalization (G3):** Works for both single-domain and multi-domain datasets by design.

---
transition: fade
---


# The Model: Zipfian Sampling

<ZipfianAnimation />

<div style="font-size: 1.1rem; max-width: 600px; margin: 1.5rem auto 0 auto; text-align: center;">
In natural language, a few words (like "the", "of", "and") are extremely common, while most words are rare. This is called a Zipfian distribution.
</div>


---
transition: fade
---

# The Model: Zipfian Sampling
Introducing ZipCal


ZipCal is a method that samples data based on the frequency of tokens, following a Zipfian distribution.


The data used for calibration is sampled according to the frequency of tokens, with more frequent tokens being more likely to be included in the calibration set.

---
transition: fade
---

# Experiments: Scalability

---
transition: fade
---

# Experiments: Quality

---
transition: fade
---

# Remarks: The Difficulty of Choosing Calibration Data

---
transition: fade
---

# Obtaining Property G3: Multi-Domain ZipCal