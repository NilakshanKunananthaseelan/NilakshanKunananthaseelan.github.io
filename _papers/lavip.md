---
title: "LaViP: Language-Grounded Visual Prompting"
paper_id: lavip
description: A parameter-efficient method that uses language to generate visual prompts for adapting vision-language models.
topics:
  - Visual prompting
  - Vision-language models
  - Model adaptation
image: /images/lavip.png
image_alt: Diagram illustrating language-grounded visual prompting with LaViP.
image_caption: LaViP reprograms a frozen visual encoder through language-grounded prompts at its input.
citation: "Kunananthaseelan, N., Zhang, J., & Harandi, M. (2024). LaViP: Language-Grounded Visual Prompting. Proceedings of the AAAI Conference on Artificial Intelligence, 38(3), 2840–2848."
bibtex: |
  @inproceedings{kunananthaseelan2024lavip,
    title     = {LaViP: Language-Grounded Visual Prompting},
    author    = {Kunananthaseelan, Nilakshan and Zhang, Jing and Harandi, Mehrtash},
    booktitle = {Proceedings of the AAAI Conference on Artificial Intelligence},
    volume    = {38},
    number    = {3},
    pages     = {2840--2848},
    year      = {2024},
    doi       = {10.1609/aaai.v38i3.28064}
  }
---

## Abstract

LaViP adapts the visual encoder of a vision-language model by learning prompts at the image input. Language provides semantic grounding for those prompts, helping the model reuse its pretrained representation without modifying or extending the encoder’s parameters.

## Core idea

Traditional visual prompting learns an input transformation from visual examples alone. LaViP incorporates class-language information when generating the prompt, connecting the downstream task to the semantic structure already present in the vision-language model.

## Capabilities

Because adaptation happens at the input, LaViP can work when the model’s internal parameters are frozen or inaccessible. The method is evaluated in few-shot adaptation, base-to-novel generalisation, and transfer-learning settings across datasets including EuroSAT, UCF101, DTD, and CLEVR.

## Why it matters

Language grounding improves the accuracy and speed of visual prompt learning while retaining the efficiency and black-box compatibility of model reprogramming.
