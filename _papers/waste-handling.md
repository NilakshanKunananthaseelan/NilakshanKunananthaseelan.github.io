---
title: "Optimizing Waste Handling with Interactive AI"
paper_id: waste-handling
description: Prompt-guided segmentation for construction and demolition waste in cluttered environments.
topics:
  - Computer vision
  - Interactive segmentation
  - Sustainable construction
citation: "Sirimewan, D., Kunananthaseelan, N., Raman, S., Garcia, R., & Arashpour, M. (2024). Optimizing waste handling with interactive AI: Prompt-guided segmentation of construction and demolition waste using computer vision. Waste Management, 190, 149–160."
bibtex: |
  @article{sirimewan2024optimizing,
    title   = {Optimizing Waste Handling with Interactive AI: Prompt-Guided Segmentation of Construction and Demolition Waste Using Computer Vision},
    author  = {Sirimewan, Diani and Kunananthaseelan, Nilakshan and Raman, Sudharshan and Garcia, Reyes and Arashpour, Mehrdad},
    journal = {Waste Management},
    volume  = {190},
    pages   = {149--160},
    year    = {2024},
    doi     = {10.1016/j.wasman.2024.09.018}
  }
---

## Abstract

Automated construction and demolition waste recognition is difficult because material categories appear in cluttered, variable environments. Generic segmentation models do not transfer reliably to this domain. This work develops an interactive pipeline that lets users guide segmentation using bounding boxes, points, or text.

## Approach

The system combines foundation-model segmentation with domain-specific prompting. Instead of requiring detailed pixel-level annotation for every object, an operator can draw a box, click a point, or describe the target material. This turns segmentation into a lightweight human–AI interaction.

## Results

The approach reaches class-wise performance of roughly 70% for several waste categories and improves on the evaluated state-of-the-art baselines by 9% on average. The different prompt modes make the system useful across varying annotation and operational constraints.

## Why it matters

Faster, more accurate material recognition can support sorting and resource recovery in waste-processing facilities. The work also illustrates how interactive foundation models can be adapted to specialised visual environments.
