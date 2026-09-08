---
title: "DIET: Machine Unlearning on a Data-Diet"
paper_id: diet
description: A retain-data-free approach to targeted machine unlearning in vision-language models using hyperbolic geometry.
topics:
  - Machine unlearning
  - Vision-language models
  - Hyperbolic learning
image: /images/diet-pipeline.png
image_alt: DIET pipeline showing image embeddings transported through hyperbolic space toward mismatched text prototypes selected by optimal transport.
image_caption: DIET moves target image embeddings along structured hyperbolic trajectories while a repulsive constraint limits interference with retained concepts.
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

<blockquote class="paper-epigraph">
  <p>“In the practical use of our intellect, forgetting is as important a function as recollecting.”</p>
  <footer>— William James, <cite>The Principles of Psychology, Vol. I</cite></footer>
</blockquote>

## Why forgetting without retain data is hard

Machine unlearning asks a trained model to remove a targeted concept without damaging everything else it has learned. Most methods protect that surrounding knowledge by training against a retain set. In practice, the original data may be private, unavailable, or too expensive to reconstruct.

The problem is sharper in vision-language models: a concept is encoded through the alignment between images and language. Breaking that alignment too aggressively can distort nearby concepts; changing it too little leaves the target knowledge intact.

<aside class="paper-callout">
  <p class="eyebrow">Core idea</p>
  <p><strong>Forget through direction, not indiscriminate destruction.</strong> DIET moves target image embeddings toward semantically mismatched prototypes at the boundary of hyperbolic space—without using retained images.</p>
</aside>

## A geometric route to selective forgetting

DIET maps image and text embeddings into a Poincaré ball. Text prompts for classes that should remain provide semantic boundary prototypes. Adaptive optimal transport assigns each forget example a suitable mismatched prototype, defining where its embedding should move rather than merely pushing it in an arbitrary direction.

Because the boundary lies at infinite geodesic distance, DIET uses the Busemann function as a finite, differentiable objective:

<div class="paper-equation" role="group" aria-label="Busemann function used by DIET">
  <div class="paper-equation__formula">δ<sub>p</sub>(z) = log(‖p − z‖² / (1 − ‖z‖²))</div>
  <p><strong>z</strong> is a forget embedding inside the Poincaré ball and <strong>p</strong> is its assigned boundary prototype. Minimising this quantity guides the embedding along a geodesic ray toward that prototype.</p>
</div>

The final objective balances three behaviours:

<div class="paper-equation" role="group" aria-label="DIET unlearning objective">
  <div class="paper-equation__formula">ℒ<sub>U</sub> = λ<sub>HYP</sub>ℒ<sub>HYP</sub> + λ<sub>OT</sub>ℒ<sub>OT</sub> + λ<sub>REP</sub>ℒ<sub>REP</sub></div>
  <p>The hyperbolic term drives forgetting, optimal transport chooses structured trajectories, and the repulsive term separates each example from unassigned prototypes to reduce cross-class interference.</p>
</div>

Only low-rank adapters in the vision encoder are updated. The text encoder supplies the prototypes, so the method does not need a retained image dataset as a training constraint.

## What the geometry changes

<figure class="paper-inline-figure">
  <img src="{{ '/images/diet-latent-space.png' | relative_url }}" alt="Latent-space comparison for CLIP, GS-LoRA, retain-free GS-LoRA, and DIET after unlearning the Shiba Inu class.">
  <figcaption>Shared CLIP space after removing “Shiba Inu.” Gradient-ascent baselines can reverse or disperse semantic structure; DIET dampens the target alignment while keeping the retained class clusters organised.</figcaption>
</figure>

The latent-space analysis makes the trade-off visible. GS-LoRA and its retain-free variant drive target similarity to negative values, while the retain-free variant also disperses the surrounding clusters. DIET instead follows a structured boundary direction and preserves the organisation of retained concepts.

## Evaluation at a glance

The study evaluates CLIP on Flowers102, OxfordPets, StanfordCars, and Food101. Each run uses 16 forget samples per concept and averages results over five randomly selected forget concepts per dataset. Lower forget-set accuracy (<em>D</em><sub>f</sub>) is better; higher test accuracy (<em>D</em><sub>t</sub>) means more general utility is retained.

<div class="paper-stat-grid" aria-label="DIET headline results">
  <div><strong>8.06%</strong><span>average forget accuracy</span></div>
  <div><strong>69.04%</strong><span>average retained utility</span></div>
  <div><strong>16</strong><span>samples per concept</span></div>
</div>

<div class="paper-table-wrap">
  <table class="paper-results">
    <thead>
      <tr><th>Method</th><th>Uses retain data?</th><th>Forget accuracy ↓</th><th>Test accuracy ↑</th></tr>
    </thead>
    <tbody>
      <tr><td>SalUn*</td><td>No</td><td>23.42%</td><td>43.53%</td></tr>
      <tr><td>GS-LoRA*</td><td>No</td><td><strong>0.00%</strong></td><td>1.73%</td></tr>
      <tr><td><strong>DIET</strong></td><td><strong>No</strong></td><td>8.06%</td><td><strong>69.04%</strong></td></tr>
      <tr><td>GS-LoRA</td><td>Yes</td><td>0.13%</td><td>71.76%</td></tr>
    </tbody>
  </table>
</div>
<p class="paper-table-note">Average accuracy across the four fine-grained datasets in Table 1. An asterisk marks a baseline adapted to run without retained data.</p>

DIET retains 25.51 percentage points more test accuracy than retain-free SalUn and comes within 2.72 points of retain-based GS-LoRA. The comparison also exposes why forget accuracy cannot be read alone: GS-LoRA* reaches zero forget accuracy but collapses overall test accuracy to 1.73%.

## What matters in the method

The ablations support two design choices. Adaptive optimal transport gives each forget example a meaningful boundary direction, while the repulsive loss protects unassigned semantic prototypes. Replacing text-derived prototypes with random boundary points weakens forgetting across every reported dataset, even when retained-class separation remains high.

Performance also depends on the number of forget examples. DIET preserves useful accuracy with very small sample sets, but its forgetting becomes less reliable below the 16-shot setting. Determining how much evidence is needed to remove a concept remains open.

## Scope and limitations

- DIET attenuates image–text alignment; it does not prove complete removal of a concept from every internal representation or downstream behaviour.
- Hyperbolic optimisation can be unstable and requires norm clipping, a repulsive regulariser, and careful hyperparameter tuning.
- Results depend on the quality of the text prototypes, and the boundary construction may be insufficient for heavily entangled concepts.
- The experiments cover targeted concept removal in CLIP-style classification settings. Applications with legal or ethical requirements for verified deletion need stronger auditing and guarantees.

## Takeaway

DIET turns retain-data-free unlearning into a geometric routing problem: choose a semantically meaningful direction for each target example, move it toward the hyperbolic boundary, and protect the concepts that should remain. The result is selective forgetting that preserves substantially more utility than the retain-free baselines tested in the paper.
