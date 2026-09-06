---
title: "OntoForm: Ontology-Grounded Semantic Data Generation for Enterprise Document Understanding"
paper_id: ontoform
description: A semantic-first framework for generating privacy-preserving enterprise document supervision from ontology-grounded entities.
affiliation: Openstream AI
topics:
  - Document understanding
  - Synthetic data
  - Ontology grounding
image: /images/ontoform-pipeline.png
image_alt: Diagram of the OntoForm pipeline from ontology map and template through entity sampling, validation, rendering, and evaluation targets.
image_caption: OntoForm compiles ontology maps and templates into hierarchical schemas, then renders validated entity records with traceable supervision signals.
citation: "Kunananthaseelan, N., Kane, B., Jain, S., Ghorbanali, M., Shiri, F., Tumuluri, R., & Haffari, G. (2026). OntoForm: Ontology-Grounded Semantic Data Generation for Enterprise Document Understanding. EMNLP 2026 Industry Track."
bibtex: |
  @inproceedings{kunananthaseelan2026ontoform,
    title     = {OntoForm: Ontology-Grounded Semantic Data Generation for Enterprise Document Understanding},
    author    = {Kunananthaseelan, Nilakshan and Kane, Benjamin and Jain, Siddharth and Ghorbanali, Mahsa and Shiri, Fatemeh and Tumuluri, Raj and Haffari, Gholamreza},
    booktitle = {Proceedings of the 2026 Conference on Empirical Methods in Natural Language Processing: Industry Track},
    year      = {2026}
  }
---

## Abstract

Enterprise forms encode related entities across fields, recurring sections, and document packets, but authentic training data is difficult to obtain because of privacy, annotation cost, and organisation-specific layouts. OntoForm is a semantic-first framework that generates enterprise form packets from a lightweight task ontology, hierarchical schemas, dependency-aware entity sampling, deterministic validation, and template bindings.

## Framework

OntoForm treats the business entity, rather than an individual page, as the primary object of generation. An ontology map defines concepts, value types, cardinalities, dependencies, and constraints. A compiler binds those layout-independent concepts to template fields, while the sampler creates a coherent latent entity record before the renderer projects it into one or more forms.

## Supervision signals

Every rendered value remains traceable to its ontology path, sampling rule, and template location. The pipeline exports filled forms, pixel-level field boxes, ontology-keyed extraction targets, grounded question-answer pairs, and validation metadata. The controlled insurance instantiation contains 706 forms, 63,318 field annotations, and 7,395 grounded question-answer pairs.

## Results

Fine-tuning vision-language models on OntoForm data improves ontology-keyed extraction F1 by 4.99 points and grounded-QA ROUGE-L by 44.1 points over zero-shot baselines. Ontology guidance improves held-out-form extraction F1 by 36.05 points overall and by 42.67 points for concepts absent from training. It also increases exact cross-form reasoning accuracy by 34.17 points.

## Why it matters

The framework provides scalable, traceable supervision without using private production documents. It also preserves cross-field and cross-document consistency, supporting document systems that must reason over complete enterprise submissions instead of treating pages as isolated visual artefacts.
