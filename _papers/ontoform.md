---
title: "OntoForm: Ontology-Grounded Semantic Data Generation for Enterprise Document Understanding"
paper_id: ontoform
description: An ontology-driven document compiler that generates linked enterprise forms and exact supervision from one validated business entity.
affiliation: Openstream AI
topics:
  - Document understanding
  - Synthetic data
  - Ontology grounding
  - Cross-form reasoning
image: /images/ontoform-semantic-pipeline.png
image_alt: OntoForm defines an ontology, samples and validates an entity record, binds its values to template fields, and renders a consistent form packet with exact supervision.
image_caption: Generate once at the semantic layer. One validated business entity anchors every rendered form and every training target.
citation: "Kunananthaseelan, N., Kane, B., Jain, S., Ghorbanali, M., Shiri, F., Tumuluri, R., & Haffari, G. (2026). OntoForm: Ontology-Grounded Semantic Data Generation for Enterprise Document Understanding. EMNLP 2026 Industry Track."
bibtex: |
  @inproceedings{kunananthaseelan2026ontoform,
    title     = {OntoForm: Ontology-Grounded Semantic Data Generation for Enterprise Document Understanding},
    author    = {Kunananthaseelan, Nilakshan and Kane, Benjamin and Jain, Siddharth and Ghorbanali, Mahsa and Shiri, Fatemeh and Tumuluri, Raj and Haffari, Gholamreza},
    booktitle = {Proceedings of the 2026 Conference on Empirical Methods in Natural Language Processing: Industry Track},
    year      = {2026}
  }
---

## Why linked forms need a shared entity

Enterprise forms are not collections of independent fields. A submission can describe the same applicant, location, exposure, or coverage across recurring sections and several related documents. Those values must agree even when labels and layouts change.

Two separate problems motivate OntoForm. Authentic training data is difficult to obtain because forms contain sensitive information and require expensive annotation. Synthetic data addresses access and labelling costs, but generating fields independently can still produce contradictory documents. Ontology grounding addresses that second problem by preserving shared facts and dependencies across a packet.

<figure class="paper-inline-figure">
  <a href="{{ '/images/ontoform-linked-forms.png' | relative_url }}"><img src="{{ '/images/ontoform-linked-forms.png' | relative_url }}" alt="Independent field generation gives the same applicant conflicting tax IDs and employee counts; entity-first generation shares one validated record across an application, endorsement, and certificate." loading="lazy"></a>
  <figcaption>Different labels can refer to the same fact. FEIN, Tax ID, and Employer ID must resolve to one semantic value across the packet. Select the diagram to view it at full size.</figcaption>
</figure>

<aside class="paper-callout">
  <p class="eyebrow">Core idea</p>
  <p><strong>Generate the entity first; render the documents second.</strong> OntoForm is an ontology-driven document compiler: one coherent business record becomes a consistent packet of forms with exact training targets.</p>
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

<figure class="paper-inline-figure">
  <a href="{{ '/images/ontoform-architecture.png' | relative_url }}"><img src="{{ '/images/ontoform-architecture.png' | relative_url }}" alt="Six stages: specify an ontology and template, compile a hierarchical schema, generate values in dependency order, validate the entity, render template-specific views, and export forms and labels. Failed validation resamples the violating subtree." loading="lazy"></a>
  <figcaption>The ontology map and template bindings require manual authoring. Entity sampling, validation, rendering, and label export then run automatically. Select the diagram to inspect the full architecture.</figcaption>
</figure>

For example, the sampler can generate a workforce total of 19 and split it into 12 full-time and 7 part-time employees. The validator checks that the counts add up before the renderer places them in any document. A shared tax identifier can appear as “FEIN” on an application and “Tax ID” on an endorsement without changing its underlying value.

## Exact supervision from the same record

<figure class="paper-inline-figure">
  <a href="{{ '/images/ontoform-supervision.png' | relative_url }}"><img src="{{ '/images/ontoform-supervision.png' | relative_url }}" alt="The FEIN value on a generated commercial application supplies its field bounding box, the ontology target organization.fein, a grounded question-answer pair, and validation metadata." loading="lazy"></a>
  <figcaption>One rendered value supplies aligned field annotations, a stable ontology target, grounded QA, and machine-checkable validation metadata.</figcaption>
</figure>

Every rendered value can be traced to an ontology path, sampling rule, and template location. That single source record produces several aligned supervision signals:

<div class="paper-artifact-grid">
  <article><h3>Filled forms</h3><p>Template-consistent documents generated without private production records.</p></article>
  <article><h3>Field annotations</h3><p>Exact values, ontology paths, page locations, and pixel-level boxes.</p></article>
  <article><h3>Grounded QA</h3><p>Questions and answers tied to visible evidence in the rendered document.</p></article>
  <article><h3>Validation metadata</h3><p>Machine-checkable evidence for types, dependencies, and cross-form consistency.</p></article>
</div>

## Reasoning across a document packet

Some questions require evidence from several forms. In the illustrated bakery scenario, the Commercial Application records vehicle use, General Liability records 1,250 annual deliveries, and Business Auto lists three delivery vans. A grounded response brings those facts together and identifies the evidence behind its answer.

<figure class="paper-inline-figure">
  <a href="{{ '/images/ontoform-cross-form-reasoning.png' | relative_url }}"><img src="{{ '/images/ontoform-cross-form-reasoning.png' | relative_url }}" alt="A bakery example combines vehicle use from a commercial application, 1,250 deliveries from general liability, and three vans from business auto. Exact reasoning rises from 18.33 to 52.50 with ontology-guided fine-tuning." loading="lazy"></a>
  <figcaption>Illustrative evidence aggregation across three forms. In the controlled study, exact reasoning improves by 34.17 percentage points over training without ontology supervision.</figcaption>
</figure>

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
      <tr><td>Does ontology supervision improve matched fine-tuning?</td><td>Extraction F1: 88.63 → 92.35</td><td><strong>+3.72</strong></td></tr>
      <tr><td>Does it correctly omit absent fields?</td><td>Accuracy including true negatives: 75.17 → 90.40</td><td><strong>+15.23</strong></td></tr>
      <tr><td>Does ontology guidance transfer to a held-out form?</td><td>F1: 60.90 → 96.95</td><td><strong>+36.05</strong></td></tr>
      <tr><td>Can the model recover concepts absent from training?</td><td>F1: 53.92 → 96.59</td><td><strong>+42.67</strong></td></tr>
      <tr><td>Can it reason across a multi-form packet?</td><td>Exact reasoning: 18.33 → 52.50</td><td><strong>+34.17</strong></td></tr>
    </tbody>
  </table>
</div>
<p class="paper-table-note">Scores are percentages; gains are percentage points. QA compares zero-shot and fine-tuned models (Table 2). Extraction and omission handling compare fine-tuning without and with ontology supervision (Table 3). Held-out-form results compare the corresponding training and prompting conditions (Table 4). Cross-form reasoning compares the two fine-tuned models without ontology at inference (Table 6). The separate extraction gain over the ontology-conditioned zero-shot baseline is +4.99 F1 (87.36 → 92.35).</p>

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
