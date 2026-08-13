---
layout: page
permalink: /research/
title: Research
description: How structural variation shapes adaptation in disease-vector mosquitoes.
nav: true
nav_order: 1
---

A chromosomal inversion flips a segment of a chromosome end to end. Recombination is suppressed between an inversion and its standard arrangement, so the genes inside travel together across generations — hundreds of them, inherited as a single unit. That makes inversions a powerful way to hold a locally adapted combination of alleles together against gene flow.

In mosquitoes this is not an abstract question. Inversions in _Anopheles gambiae_ track aridity across West Africa; in _Aedes aegypti_ they fall near loci tied to host preference. If we want to know why one population bites humans and another bites birds, or why one survives a temperate winter, chromosome structure is one of the places to look.

Finding and validating these rearrangements takes both a bench and a terminal. My work runs the full pipeline:

<style>
  /* Wet/dry chips are filled blocks, so they need enough contrast against BOTH the
     page background and their own white label. The dark-mode pair is lightened:
     #861F41 sits at only 1.9:1 against #1c1c1d and reads as a muddy smudge. */
  .pipeline {
    --pl-wet: #861F41; /* white label 9.2:1 */
    --pl-dry: #1F5D6B; /* white label 7.5:1 */
    margin: 1.8rem 0 2.2rem;
    border: 1px solid var(--global-divider-color);
    border-radius: 6px;
    padding: 1.4rem 1.2rem;
    background: var(--global-card-bg-color, transparent);
  }
  html[data-theme="dark"] .pipeline {
    --pl-wet: #A83E5F; /* white label 5.9:1, 2.9:1 vs page */
    --pl-dry: #2E7D8F; /* white label 4.8:1, 3.6:1 vs page */
  }
  .pipeline-legend {
    display: flex; flex-wrap: wrap; gap: 1.1rem;
    font-size: 0.78rem; letter-spacing: 0.04em; text-transform: uppercase;
    color: var(--global-text-color-light); margin-bottom: 1.1rem;
  }
  .pipeline-legend span { display: inline-flex; align-items: center; gap: 0.4rem; }
  .pipeline-legend i { width: 11px; height: 11px; border-radius: 2px; display: inline-block; }
  .pl-wet { background: var(--pl-wet); }
  .pl-dry { background: var(--pl-dry); }
  .pipeline-step { display: flex; align-items: flex-start; gap: 0.85rem; }
  .pipeline-step .tag {
    flex: 0 0 46px; text-align: center; font-size: 0.62rem; letter-spacing: 0.06em;
    text-transform: uppercase; padding: 2px 0; border-radius: 3px; margin-top: 0.22rem;
    color: #fff;
  }
  .pipeline-step .tag.wet { background: var(--pl-wet); }
  .pipeline-step .tag.dry { background: var(--pl-dry); }
  .pipeline-step .lbl { font-size: 0.94rem; line-height: 1.45; }
  .pipeline-step .lbl small { display: block; color: var(--global-text-color-light); font-size: 0.8rem; }
  .pipeline-link { width: 1px; height: 14px; margin-left: 23px; background: var(--global-divider-color); }
  @media (max-width: 480px) {
    .pipeline-step .tag { flex-basis: 40px; font-size: 0.56rem; }
    .pipeline-link { margin-left: 20px; }
  }
</style>

<div class="pipeline">
  <div class="pipeline-legend">
    <span><i class="pl-wet"></i> Wet lab</span>
    <span><i class="pl-dry"></i> Dry lab</span>
  </div>
  <div class="pipeline-step"><span class="tag wet">Wet</span><span class="lbl">Field collection and colony maintenance<small>Wild populations across a geographic range, plus reference colonies</small></span></div>
  <div class="pipeline-link"></div>
  <div class="pipeline-step"><span class="tag wet">Wet</span><span class="lbl">Hi-C library preparation<small>Proximity ligation captures which sequences sit near each other in the nucleus</small></span></div>
  <div class="pipeline-link"></div>
  <div class="pipeline-step"><span class="tag dry">Dry</span><span class="lbl">Genome assembly and scaffolding<small>Contact maps resolve chromosome-scale order; inversions leave a characteristic signal</small></span></div>
  <div class="pipeline-link"></div>
  <div class="pipeline-step"><span class="tag wet">Wet</span><span class="lbl">FISH physical validation<small>Fluorescent probes place the candidate breakpoints on real chromosomes</small></span></div>
  <div class="pipeline-link"></div>
  <div class="pipeline-step"><span class="tag wet">Wet</span><span class="lbl">PCR breakpoint genotyping<small>A cheap assay that scales the finding from a few genomes to whole populations</small></span></div>
  <div class="pipeline-link"></div>
  <div class="pipeline-step"><span class="tag dry">Dry</span><span class="lbl">Population genomics<small>F<sub>ST</sub>, PCA, and AMOVA relate inversion frequency to geography and environment</small></span></div>
  <div class="pipeline-link"></div>
  <div class="pipeline-step"><span class="tag dry">Dry</span><span class="lbl">Ecological and vectorial interpretation<small>What the structure means for host preference, seasonality, and control</small></span></div>
</div>

The steps alternate between bench and terminal on purpose. A Hi-C signal that looks like an inversion can be an assembly artifact; FISH tells you whether it is physically real. A validated inversion in two genomes tells you nothing about whether it matters; population-scale genotyping does.

---

## Chromosomal inversions in the _Culex pipiens_ complex

_Dissertation core · manuscript in preparation_

**The question.** The _Culex pipiens_ complex contains forms that look nearly identical and behave completely differently. _Cx. pipiens_ prefers birds; _Cx. quinquefasciatus_ readily bites mammals; the _molestus_ form breeds underground, mates in confined spaces, and skips diapause. Where they overlap they hybridize — which raises the question of how these behavioral and ecological differences persist at all. Suppressed recombination inside inversions is one plausible answer.

**The approach.** I used Hi-C proximity ligation to detect candidate rearrangements between complex members, confirmed them physically by FISH, and developed PCR breakpoint assays to genotype them across populations.

**What I am testing.** Whether inversion frequencies track ecological variables across North American populations, and whether the rearranged regions contain genes plausibly linked to host preference and diapause. This work was presented at ASTMH in 2024, and the host-preference results have been accepted for the Student 10-Minute Presentation Competition at [Entomology 2026](https://entsoc.org/events/annual-meeting) in November. A manuscript is in preparation.

## Chromosome-scale genome assembly of _Aedes albopictus_

_Manuscript in preparation_

**The question.** _Aedes albopictus_, the Asian tiger mosquito, has spread across every inhabited continent in a few decades and transmits dengue, chikungunya, and Zika. Its genome is large and highly repetitive, which has kept assemblies fragmented and made structural variants hard to see.

**The approach.** Trio-binning — parental Illumina reads used to partition offspring Nanopore long reads by haplotype — followed by Hi-C scaffolding to chromosome scale. Candidate inversions from the contact map were confirmed by FISH physical mapping.

**What it enables.** A chromosome-scale, haplotype-resolved reference makes structural variation visible in a species where it has largely been invisible, and gives inversion genotyping in this vector a foundation to build on.

## Comparative inversion landscapes across vector mosquitoes

_Published in [Genome Biology and Evolution](https://doi.org/10.1093/gbe/evaf118), 2025_

**The question.** _Aedes aegypti_ is the principal vector of dengue, yellow fever, Zika, and chikungunya, but its polytene chromosomes are too poorly structured for the classical cytogenetic methods that mapped inversions in _Anopheles_. Its inversions were essentially uncharted.

**The approach.** As part of an international collaboration spanning nine countries, we applied Hi-C based inversion discovery across the species' range, from its ancestral African populations to globally invasive ones.

**What we found.** Inversions are present and polymorphic, and their distribution is structured rather than random — consistent with a role in the evolution of this vector. Setting the _Culex_ and _Aedes_ results side by side is what makes the comparative question tractable: whether inversions are a recurring mechanism of adaptation across vector mosquitoes, or something each lineage arrived at separately.
