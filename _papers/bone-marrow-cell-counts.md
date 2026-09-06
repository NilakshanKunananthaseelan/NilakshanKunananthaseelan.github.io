---
title: "Machine-based Detection and Classification for Bone Marrow Aspirate Differential Counts"
paper_id: bone-marrow-cell-counts
description: A two-stage machine-learning pipeline for detecting and classifying cells in bone-marrow aspirate images.
topics:
  - Digital pathology
  - Cell detection
  - Medical imaging
image: /images/wbc.png
image_alt: Example bone-marrow cells detected and classified by the computer-vision pipeline.
image_caption: The pipeline separates cell detection from fine-grained cell classification.
citation: "Chandradevan, R., Aljudi, A. A., Drumheller, B. R., Kunananthaseelan, N., Amgad, M., Gutman, D. A., Cooper, L. A. D., & Jaye, D. L. (2020). Machine-based detection and classification for bone marrow aspirate differential counts: Initial development focusing on nonneoplastic cells. Laboratory Investigation, 100(1), 98–109."
bibtex: |
  @article{chandradevan2020machine,
    title   = {Machine-Based Detection and Classification for Bone Marrow Aspirate Differential Counts: Initial Development Focusing on Nonneoplastic Cells},
    author  = {Chandradevan, Ramraj and Aljudi, Ahmed A. and Drumheller, Bradley R. and Kunananthaseelan, Nilakshan and Amgad, Mohamed and Gutman, David A. and Cooper, Lee A. D. and Jaye, David L.},
    journal = {Laboratory Investigation},
    volume  = {100},
    number  = {1},
    pages   = {98--109},
    year    = {2020},
    doi     = {10.1038/s41374-019-0325-7}
  }
---

## Abstract

Bone-marrow aspirate differential cell counts are important in the classification of haematological disorders, but manual counting is slow and subject to observer variation. This study develops a machine-learning system for detecting and classifying cells in digitised bone-marrow aspirate smears.

## Pipeline

More than 10,000 cells were manually annotated using a web-based digital-pathology system. The model uses a two-stage design: first locating cells in whole-slide imagery, then classifying the detected cells into the categories used for clinical differential counts.

## Results

In six-fold cross-validation on non-neoplastic samples, the system achieved a precision–recall AUC of 0.959 for detection and a ROC AUC of 0.982 for classification. Tests on a small set of acute myeloid leukaemia and multiple myeloma samples showed similar early performance.

## Why it matters

The work demonstrates the feasibility of objective, machine-assisted bone-marrow differential counting and provides an early foundation for clinically validated automated workflows.
