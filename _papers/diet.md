---
title: "DIET: Machine Unlearning on a Data-Diet"
paper_id: diet
description: A retain-data-free approach to targeted machine unlearning in vision-language models using hyperbolic geometry.
topics:
  - Machine unlearning
  - Vision-language models
  - Hyperbolic learning
citation: "Kunananthaseelan, N., Wu, J., Le, T., Haffari, G., & Harandi, M. (2026). DIET: Machine Unlearning on a Data-Diet. Proceedings of the AAAI Conference on Artificial Intelligence, 40(27), 22698–22706."
bibtex: |
  @inproceedings{kunananthaseelan2026diet,
    title     = {DIET: Machine Unlearning on a Data-Diet},
    author    = {Kunananthaseelan, Nilakshan and Wu, Jing and Le, Trung and Haffari, Gholamreza and Harandi, Mehrtash},
    booktitle = {Proceedings of the AAAI Conference on Artificial Intelligence},
    volume    = {40},
    number    = {27},
    pages     = {22698--22706},
    year      = {2026},
    doi       = {10.1609/aaai.v40i27.39431}
  }
---

## Abstract

Machine unlearning aims to remove targeted knowledge from a trained model. Most existing methods use retained training data to protect the model’s remaining utility, which can be difficult to access for privacy and scalability reasons. DIET studies the harder retain-data-free setting for vision-language models.

## Core idea

DIET formulates unlearning in hyperbolic space. Forget embeddings are moved towards semantically mismatched prototypes at the boundary of the Poincaré ball, where geodesic distance grows rapidly. A Busemann-guided objective controls this trajectory, while optimal transport selects suitable mismatched prototypes for individual samples.

## Results

Across Flowers102, OxfordPets, and StanfordCars, the method reaches an average forget accuracy of 8.06% while preserving 69.04% utility using 16 samples per concept. The experiments show a substantial improvement over retain-free baselines and competitive performance against methods that use retained data.

## Why it matters

The work provides a geometric route to selective forgetting without requiring the original retain set. This is useful when data access is restricted or when multimodal training data is too expensive to reconstruct.
