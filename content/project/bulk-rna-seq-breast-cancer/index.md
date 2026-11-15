---
title: "Transcriptomic response to neoadjuvant chemotherapy"
subtitle: "Bulk RNA-seq of pre-treatment breast tumours (GSE192341)"
excerpt: "DESeq2, xCell cell-type enrichment and pathway analysis comparing breast tumours that reached pathological complete response with those that did not."
date: 2026-02-04
author: "Sourabh Kumar Daksh"
draft: false
weight: 8
tags:
  - RNA-seq
  - DESeq2
  - breast cancer
  - R
categories:
  - Transcriptomics
layout: single
links:
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/bioinfosourabh/Bulk-RNA-Seq
---

Which features of a breast tumour before treatment predict a pathological complete response (pCR) to neoadjuvant chemotherapy? Using 85 pre-treatment tumours from GEO GSE192341 (24 pCR, 61 residual disease), this R workflow covers:

- count-matrix and metadata construction from GEO, and input validation;
- DESeq2 with apeglm fold-change shrinkage, and VST/PCA/sample-distance QC;
- xCell enrichment of immune and stromal cell types;
- over-representation and GSEA with Hallmark, GO and Reactome gene sets.

Proliferation (E2F targets, G2M checkpoint, MYC) and interferon response were enriched in tumours that reached pCR, and oestrogen response in those with residual disease. The pipeline runs end to end on bundled example data in CI.
