---
title: "Mitochondrial variants and heteroplasmy"
subtitle: "The GATK mitochondria workflow in Nextflow"
excerpt: "Calls mitochondrial SNVs, indels and heteroplasmy levels from whole-genome BAM/CRAM, with shifted-reference calling of the control region, NuMT filtering and Haplogrep 3 haplogroups."
date: 2026-11-15
author: "Sourabh Kumar"
draft: false
weight: 5
tags:
  - mitochondria
  - heteroplasmy
  - GATK
  - Nextflow
categories:
  - Pipelines
layout: single
links:
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/bioinfosourabh/mito-variant-calling
---

The mitochondrial genome is circular, so variants in the control region, which spans the reference's start and end, are missed by a standard alignment. Following the GATK best-practice mitochondria workflow (Laricchia et al., 2022), this pipeline realigns chrM reads to both the standard reference and a copy rotated by 8 kb, and calls each half of the genome where it is not split by the reference's ends:

- Mutect2 in mitochondria mode on both alignments, with lift-over of shifted calls back to standard coordinates;
- filtering for known artefact sites, nuclear mitochondrial segments (NuMTs, using autosomal coverage) and low heteroplasmy;
- haplogroup assignment with Haplogrep 3 and a per-sample heteroplasmy report.

A helper builds the shifted reference, chain file and intervals from any genome FASTA. On simulated data both haplogroups were assigned correctly, and heteroplasmies were called close to their simulated levels.
