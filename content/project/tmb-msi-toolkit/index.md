---
title: "TMB and MSI from tumour panels"
subtitle: "Tumour mutational burden and microsatellite instability with auditable filtering"
excerpt: "Tumour mutational burden over a depth-defined callable territory, with tumour-only germline removal using gnomAD 4.1 and Indian population frequencies, and MSI status from MSIsensor-pro or MSIsensor2."
date: 2026-11-15
author: "Sourabh Kumar Daksh"
draft: false
weight: 2
tags:
  - TMB
  - MSI
  - somatic variants
  - Mutect2
  - Python
categories:
  - Cancer genomics
  - Pipelines
layout: single
links:
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/bioinfosourabh/tmb-msi-toolkit
---

Tumour mutational burden (TMB) and microsatellite instability (MSI) guide immunotherapy decisions, but both depend heavily on how variants are filtered, especially when there is no matched normal. This toolkit packages the TMB/MSI step of a tumour-only somatic panel pipeline:

- **Callable territory measured per sample:** panel coding bases with depth ≥ 100 in that sample (mosdepth + bedtools), so the denominator reflects what was actually sequenced.
- **Germline removal without a normal:** population allele frequency ≤ 0.001 across gnomAD 4.1 (including group-max and South Asian) and the Regeneron Million Exome data (including its Indian group), plus VAF bands typical of germline variants.
- **Artefact handling:** Mutect2 artefact filters are dropped, with ClinVar/COSMIC rescue for known hotspots.
- **Auditable output:** every allele carries the reasons it was or was not counted, and a filter funnel shows how many variants each rule removed.
- **MSI:** MSIsensor-pro against a panel-specific baseline built from normals, or MSIsensor2 tumour-only models. Samples with too few evaluable sites are reported as indeterminate.

Default thresholds (VAF ≥ 5%, ≥ 5 alt reads, TMB-high at 10 mut/Mb, synonymous variants counted) live in one configuration file shared by the Python CLI and the shell steps. 61 tests cover the filters.
