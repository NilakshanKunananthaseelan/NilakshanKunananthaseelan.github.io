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

## Why enterprise forms are hard

Enterprise forms are not collections of independent fields. A submission can describe the same applicant, location, exposure, or coverage across recurring sections and several related documents. Those values must agree even when labels and layouts change.

Authentic training data is difficult to obtain because forms contain sensitive information, require expensive annotation, and vary across organisations. Existing synthetic pipelines can make plausible pages, but independently filled fields may still contradict one another.

<aside class="paper-callout">
  <p class="eyebrow">Core idea</p>
  <p><strong>Generate the entity first; render the documents second.</strong> OntoForm models a coherent business record before projecting it into any template.</p>
</aside>

## A semantic-first pipeline

OntoForm begins with an ontology map and a document template. The ontology compiler turns stable domain concepts into a hierarchical schema; the entity sampler creates a latent record; a deterministic validator checks its constraints; and the renderer projects that record into one or more forms. Because the semantic record is shared, related documents inherit the same underlying facts.

<div class="paper-equation" role="group" aria-label="Ontology representation">
  <div class="paper-equation__formula">𝒪 = (𝒞, 𝒫, ℛ, 𝒦)</div>
  <p><strong>𝒞</strong> contains concept classes, <strong>𝒫</strong> their properties, <strong>ℛ</strong> semantic relations, and <strong>𝒦</strong> the constraints, dependencies, and sampling rules. The representation is intentionally lightweight and independent of page layout.</p>
</div>

The compiler binds ontology paths to template fields, page indices, value types, and bounding boxes. Sampling then follows the dependency graph rather than filling fields independently:

<div class="paper-equation" role="group" aria-label="Dependency-aware entity sampling">
  <div class="paper-equation__formula">p(z | s) = ∏<sub>v∈order(G)</sub> p(z<sub>v</sub> | z<sub>pa(v)</sub>, s)</div>
  <p><strong>z</strong> is the complete entity record, <strong>s</strong> is an optional business scenario, and <strong>pa(v)</strong> contains the declared parents of field <strong>v</strong>. In plain language, every dependent value is sampled only after the facts it relies on are known.</p>
</div>

A candidate record is accepted only when the validator confirms its types, required fields, cardinalities, temporal rules, and cross-document invariants. When possible, OntoForm resamples only the invalid subtree instead of discarding the whole record.

## Traceable supervision, not just plausible pages

<figure class="paper-inline-figure">
  <img src="{{ '/images/ontoform-ontology-paths.png' | relative_url }}" alt="A surrogate commercial insurance form with red callouts connecting visible values to ontology paths.">
  <figcaption>Ontology-path callouts connect visible fields to stable semantic targets. Each value is exported with its ground truth and pixel-level bounding box.</figcaption>
</figure>

Every rendered value can be traced to an ontology path, sampling rule, and template location. That single source record produces several aligned supervision signals:

<div class="paper-artifact-grid">
  <article><h3>Filled forms</h3><p>Template-consistent documents generated without private production records.</p></article>
  <article><h3>Field annotations</h3><p>Exact values, ontology paths, page locations, and pixel-level boxes.</p></article>
  <article><h3>Grounded QA</h3><p>Questions and answers tied to visible evidence in the rendered document.</p></article>
  <article><h3>Validation metadata</h3><p>Machine-checkable evidence for types, dependencies, and cross-form consistency.</p></article>
</div>

## Evaluation at a glance

The controlled insurance study covers three surrogate form types: Commercial Application, General Liability, and Business Auto. Entity-level splits keep the same sampled business profile from appearing in both training and test sets.

<div class="paper-stat-grid" aria-label="Evaluation corpus scale">
  <div><strong>706</strong><span>rendered forms</span></div>
  <div><strong>63,318</strong><span>field annotations</span></div>
  <div><strong>7,395</strong><span>grounded QA pairs</span></div>
</div>

<div class="paper-table-wrap">
  <table class="paper-results">
    <thead>
      <tr><th>Question</th><th>Comparison</th><th>Measured gain</th></tr>
    </thead>
    <tbody>
      <tr><td>Does synthetic supervision help grounded QA?</td><td>ROUGE-L: 53.1 → 97.2</td><td><strong>+44.1</strong></td></tr>
      <tr><td>Does it improve ontology-keyed extraction?</td><td>F1: 87.36 → 92.35</td><td><strong>+4.99</strong></td></tr>
      <tr><td>Does ontology guidance transfer to a held-out form?</td><td>F1: 60.90 → 96.95</td><td><strong>+36.05</strong></td></tr>
      <tr><td>Can the model recover concepts absent from training?</td><td>F1: 53.92 → 96.59</td><td><strong>+42.67</strong></td></tr>
      <tr><td>Can it reason across a multi-form packet?</td><td>Exact reasoning: 18.33 → 52.50</td><td><strong>+34.17</strong></td></tr>
    </tbody>
  </table>
</div>
<p class="paper-table-note">Scores are percentages or percentage-point gains. Comparisons follow the matched conditions reported in Tables 2–6 of the paper.</p>

## What ontology grounding changes

The strongest gains appear when the layout or semantic inventory changes. On a held-out Business Auto form, ontology guidance adds 36.05 F1 points across all fields and 42.67 points on concepts that never appear in the training forms.

The same pattern holds for two unseen surrogate lines of business. Canonical path-value F1 rises from 4.1 to 91.4 for Workers’ Compensation and from 5.2 to 80.2 for Commercial Property. Hallucination falls from 95.1% to 1.0% and from 93.5% to 0.1%, respectively. These experiments remain inside the controlled synthetic pipeline, but they isolate the benefit of stable semantic paths when surface forms change.

## Scope and limitations

- The study uses digitally rendered, template-consistent surrogate insurance forms; it does not establish transfer to authentic enterprise documents.
- The evaluation does not yet cover handwriting, stamps, skew, OCR errors, low-resolution scans, missing fields, or continuously evolving layouts.
- OntoForm uses a lightweight task ontology rather than full OWL or description-logic reasoning, and authoring its maps, validators, and bindings requires domain expertise.
- Strong synthetic-data results are not evidence that an automated system is safe for consequential insurance decisions. Production use still requires human review, shift monitoring, and fairness evaluation.

## Takeaway

OntoForm reframes enterprise forms as layout-specific views of a shared semantic entity. That shift makes it possible to generate scalable, privacy-preserving supervision while retaining the cross-field and cross-document consistency required for extraction, grounded question answering, and multi-form reasoning.
