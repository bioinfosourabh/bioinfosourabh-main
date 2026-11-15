---
title: "Trio exome analysis for rare disease"
subtitle: "Inheritance-based filtering of proband–parent exomes"
excerpt: "Germline calling for a proband and both parents, followed by filters for de novo, recessive, X-linked, dominant and parental mosaic candidate variants."
date: 2025-04-02
author: "Sourabh Kumar"
draft: false
weight: 7
tags:
  - rare disease
  - trio
  - WES
  - Bash
categories:
  - Clinical genomics
  - Pipelines
layout: single
links:
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/bioinfosourabh/Trio-Exome-Analysis-Pipeline
---

Trio sequencing narrows thousands of variants to a short candidate list by asking how each one is inherited. The pipeline runs GATK germline calling for the proband and both parents, then filters the joint VCF for:

- de novo variants;
- autosomal recessive (homozygous) variants;
- X-linked recessive variants in a male proband;
- inherited autosomal dominant variants;
- possible parental mosaicism, where a parent carries the variant at low allele fraction.

The scripts are configured from one file, check their dependencies, log every step and skip finished steps when re-run. This approach grew out of my rare-disease exome work at AIIMS New Delhi.
