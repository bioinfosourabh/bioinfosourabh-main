---
title: "Sequenza 4 silently ignores scarHRD's segmentation settings"
subtitle: "A version mismatch that compresses high HRD scores"
excerpt: "scarHRD passes gamma and kmin to Sequenza, but Sequenza 4.0.0 no longer uses them and does not complain. On public reference data, this pulled high HRD scores down by about 24 points on average."
date: 2026-11-15
author: "Sourabh Kumar Daksh"
draft: false
tags:
  - HRD
  - Sequenza
  - scarHRD
  - reproducibility
categories:
  - Cancer genomics
layout: single
---

While validating an [HRD scoring pipeline](/project/hrd-scoring/) against published scores, I kept seeing the same pattern: tumours with high reported HRD scores came out well below their reference values, while low scores matched reasonably well. The cause turned out not to be biology or sequencing depth. It was a version mismatch between two R packages, and neither of them raised an error.

## What happens

[scarHRD](https://github.com/sztup/scarHRD) (Sztupinszki et al., 2018) computes the genomic-scar HRD score (LOH + TAI + LST) from [Sequenza](https://cran.r-project.org/package=sequenza) allele-specific copy number. Internally it calls `sequenza.extract()` with the segmentation settings it was designed and published with: `gamma = 60` and `kmin = 50`.

In Sequenza 2.x and 3.x, `gamma` and `kmin` control a piecewise-constant segmentation through the `copynumber` package. In the Sequenza 4.0.0 build I had installed, `sequenza.extract()` segments differently and has no `gamma` or `kmin` arguments at all. Because the function also accepts `...`, R swallows both arguments without a warning. Every run therefore used Sequenza 4's own segmentation, whatever settings I passed.

I noticed only when a grid of different gamma/kmin settings gave **identical scores to the last digit** for every sample.

## Why it matters for the score

LST and TAI are counted from breakpoints, so the segmentation decides the score. On nine reference tumours with published HRD scores (the KB/GW standards in PRJNA850105), running the same seqz files through both versions gave:

| | Sequenza 4.0.0 | Sequenza 3.0.0 (scarHRD as designed) |
|---|---|---|
| Mean absolute gap to the reported score | 16 | 10 |
| Mean gap for high-HRD tumours | −24 | −12 |

The positive/negative calls at the usual cut-off of 42 did not change on this small set, but scores were compressed towards the middle. That matters for anything that uses the number itself, and near the cut-off it would change calls.

## How to avoid it

- Run scarHRD with **Sequenza 3.0.0** (the last version on CRAN) in its own environment, for example `conda create -n seq3 -c conda-forge -c bioconda r-sequenza=3.0.0 bioconductor-copynumber`.
- Check before scoring: `c("gamma", "kmin") %in% names(formals(sequenza::sequenza.extract))` should return `TRUE TRUE`.
- When you test settings, confirm that the **number of segments actually changes** between settings. Identical outputs are a warning sign, not a sign of robustness.

Two more scarHRD details caught me out on hg38: it asks Sequenza for chromosomes `chr1`–`chr24`, so with `chrX`/`chrY` naming the score is effectively autosomes-only; and it passes `mufreq.treshold` to `sequenza.fit()`, which Sequenza 3 no longer accepts. My [pipeline](https://github.com/bioinfosourabh/hrd-scoring) handles all three: it refuses to run on Sequenza ≥ 4, scores chr1–22 explicitly, and patches out the removed argument.

With these fixes, matched tumour–normal scoring agreed with the published HRD call for 90 of 97 public tumours (Lin's concordance 0.966). The full validation is on the [project page](/project/hrd-scoring/).
