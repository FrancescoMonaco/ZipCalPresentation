---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: 
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
}
</style>


# <span class="zipcal-title">Frrequenccy Mat terss</span>

Fast Model-Agnostic Data Curation for Pruning and Quantization

<div class="absolute bottom-10">
  <span class="font-700">
    Francesco Pio Monaco, Elia Cunegatti, Flavio Vella, Giovanni Iacca April 2026
  </span>
</div>

---
transition: fade
---

# The Setting: Model Compression
What is Model Compression?

---
transition: fade
---

# The Setting: Model Compression
Pruning & Quantization

---
transition: fade
---

# The Setting: Calibration Data for Model Compression
Desired Properties

- scalability (G1), i.e., capable of processing massive corpora with minimal
computational overhead; 
- model-agnostic (G2), i.e.,
capable of identifying the most informative examples from a corpus without relying on expensive
model passes;
- inter-domain generalization (G3), i.e., being capable of synthesizing
both Single-Domain and Multi-Domain corpora
settings by design.

---
transition: fade
---

# The Model: Zipfian Sampling
Languanges and frequency of words


---
transition: fade
---

# The Model: Zipfian Sampling
Introducing ZipCal


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