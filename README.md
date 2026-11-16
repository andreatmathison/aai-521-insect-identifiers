# Automated Butterfly Species Classification
**University of San Diego — Shiley-Marcos School of Engineering**  
**Course:** AAI-521, Group 4 "Insect Identifiers!"

---

## Project Overview & Problem Definition

### What is the problem we are solving?
Global pollinator populations—particularly Lepidoptera (butterflies)—are experiencing severe declines driven by habitat fragmentation, pesticide usage, and climate change. Tracking species distribution and biodiversity relies heavily on manual entomological surveys and expert taxonomic verification, which are slow, labor-intensive, and bottlenecked by a shortage of domain specialists. This project implements an end-to-end computer vision classification and feature engineering pipeline capable of identifying **75 distinct butterfly species** from natural field imagery.

### Why does this problem need to be solved?
Butterflies serve as vital pollinators and sensitive ecological bio-indicators. Rapid, scalable, and non-invasive biodiversity monitoring is critical for conservation biology, agricultural ecosystem tracking, and ecological modeling. Automating taxonomic identification empowers citizen science platforms, automated wildlife camera traps, and researchers to classify thousands of field observations in real time.

### What aspect of the problem does our computer vision pipeline solve?
Field photographs of butterflies exhibit extreme variability in wing posture (dorsal vs. ventral views), natural outdoor lighting, background foliage clutter, scale, and inter-species visual mimicry. Our pipeline addresses these challenges through:
1. **Programmatic Data Readiness & Deduplication:** Verifying byte-stream integrity, standardizing color channels, and eliminating cross-split leakage via MD5 cryptographic file hashing.
2. **Deterministic Spatial & Radiometric Pre-Processing:** Applying aspect-ratio preserving resizing ($224 \times 224$) with reflection padding to preserve wing-to-thorax geometry, paired with **CIE LAB Luminance CLAHE** to normalize outdoor canopy shadows without distorting species coloration.
3. **Computer Vision Feature Engineering:** Extracting 16 quantitative radiometric, color-space, morphological, and spatial-frequency features per image to support both pure deep learning backbones and hybrid multi-modal fusion models.
4. **Deep Learning Modeling & Validation:** Training, validating, and benchmarking modern convolutional (CNN) and attention-based (Vision Transformer) architectures under domain-specific spatial and photometric augmentations.

---

## Dataset Description

* **Source:** [Kaggle Butterfly Image Classification Dataset (`phucthaiv02/butterfly-image-classification`)](https://www.kaggle.com/datasets/phucthaiv02/butterfly-image-classification)
* **Total Labeled Images:** 6,499 raw field images (deduplicated via MD5 hash audit during Step 2A)
* **Target Classes:** 75 butterfly species (Order: *Lepidoptera*), mapped to integer labels `0` through `74` in `class_info.json`
* **Partitioning Strategy:** Stratified **80% Train / 10% Validation / 10% Held-Out Test** split across all 75 classes, with zero cross-split hash overlap.
