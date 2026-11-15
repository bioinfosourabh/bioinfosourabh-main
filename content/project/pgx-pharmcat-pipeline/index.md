---
title: "Pharmacogenomics from exomes with PharmCAT"
subtitle: "Star-allele diplotypes, phenotypes and guideline recommendations"
excerpt: "A laboratory workflow around PharmCAT 3.2.0 for WES data: input checks, CYP2D6 outside calls, QC at pharmacogene positions and concordance checks against GeT-RM reference samples."
date: 2026-11-15
author: "Sourabh Kumar Daksh"
draft: false
weight: 6
tags:
  - pharmacogenomics
  - PharmCAT
  - CPIC
  - WES
categories:
  - Clinical genomics
  - Pipelines
layout: single
links:
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/bioinfosourabh/pgx-pharmcat-pipeline
---

PharmCAT turns a VCF into star-allele diplotypes, phenotypes and CPIC/DPWG prescribing recommendations. Using it on whole exomes in a laboratory needs more around it, and this repository provides that:

- a version-pinned PharmCAT container, with the image digest and version recorded for every run;
- input checks for GRCh38, `chr`-prefixed contigs and lift-over;
- CYP2D6 called from BAM with Aldy or Stargazer and passed in as a PharmCAT outside call, because PharmCAT cannot call CYP2D6 from a VCF;
- QC of depth and genotype quality at all 1,207 PharmCAT positions. **Absent is not reference:** a variant-only VCF leaves PGx positions uncalled, and the QC makes this visible;
- per-sample summaries and a concordance check against GeT-RM reference genotypes.
