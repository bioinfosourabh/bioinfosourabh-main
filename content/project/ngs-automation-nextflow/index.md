---
title: "Germline and somatic variant calling in Nextflow"
subtitle: "GATK4 best practices as a DSL2 pipeline"
excerpt: "A Nextflow DSL2 pipeline for germline (HaplotypeCaller, joint genotyping) and somatic (Mutect2 tumour-normal or tumour-only) short-variant calling from FASTQ."
date: 2026-11-15
author: "Sourabh Kumar Daksh"
draft: false
weight: 4
tags:
  - Nextflow
  - GATK
  - variant calling
  - WES
  - WGS
categories:
  - Pipelines
layout: single
links:
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/bioinfosourabh/ngs-automation-nextflow
---

A Nextflow (DSL2) pipeline that takes paired-end FASTQ files to filtered germline and somatic VCFs, following the GATK4 best-practice workflows:

- fastp trimming → BWA-MEM2 alignment per lane → duplicate marking → base quality score recalibration;
- **germline:** HaplotypeCaller GVCFs, joint genotyping with GenomicsDBImport or CombineGVCFs, then hard filters or VQSR;
- **somatic:** Mutect2 against a matched normal or tumour-only with a panel of normals, orientation-bias model, contamination estimate and FilterMutectCalls;
- normalised PASS VCFs, optional Ensembl VEP annotation, coverage with mosdepth and a MultiQC report.

Every process runs in a pinned container, the work is scattered over genomic intervals, and runs resume with `-resume`. On simulated test data, germline genotypes matched the truth set exactly and the somatic branch recovered the planted SNVs with no false positives.
