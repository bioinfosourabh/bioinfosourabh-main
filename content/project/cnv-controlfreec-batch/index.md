---
title: "Cohort CNV calling with Control-FREEC"
subtitle: "Sample-sheet-driven copy-number analysis for many tumours"
excerpt: "Runs Control-FREEC across a cohort from one sample sheet and one config template, then adds significance testing, plots and a merged cohort CNV table."
date: 2026-11-15
author: "Sourabh Kumar"
draft: false
weight: 3
tags:
  - CNV
  - Control-FREEC
  - Nextflow
  - Bash
categories:
  - Cancer genomics
  - Pipelines
layout: single
links:
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/bioinfosourabh/cnv-controlfreec-batch
---

Control-FREEC needs one hand-written configuration file per sample, which becomes error-prone across a cohort. This repository generates those files from a **sample sheet and a single template**, runs FREEC on every sample, and adds the post-processing from the FREEC distribution: Wilcoxon/Kolmogorov–Smirnov significance tests, ratio and BAF plots, and BED/Circos exports. All calls are then merged into cohort tables.

- Tumour-normal pairs and tumour-only samples; exome or panel data with a capture BED, and whole genomes.
- A helper pairs `S*_SO.bam` tumours with `S*_GL.bam` normals automatically.
- Two ways to run: a containerised, resumable Nextflow pipeline, or Bash scripts for a single server.
- Fixes two common configuration pitfalls: `makePileup` must point to a file, and exome mode needs per-chromosome FASTA files.

Tested on simulated data with planted gains and losses, which were recovered in every sample.
