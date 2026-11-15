---
title: "Single-cell RNA-seq with Seurat and SingleR"
subtitle: "From count matrix to annotated cell types"
excerpt: "A Seurat v5 workflow for droplet single-cell RNA-seq: QC, normalisation, clustering, marker genes, SingleR annotation and T/NK and myeloid sub-analysis."
date: 2025-03-16
author: "Sourabh Kumar Daksh"
draft: false
weight: 9
tags:
  - single-cell
  - scRNA-seq
  - Seurat
  - R
categories:
  - Transcriptomics
layout: single
links:
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/bioinfosourabh/Single-Cell-Analysis
---

A configurable R workflow for 10x Genomics single-cell RNA-seq:

1. QC on detected genes, UMI counts and mitochondrial and ribosomal fractions;
2. LogNormalize or SCTransform v2, highly variable genes, PCA, UMAP and t-SNE;
3. graph-based clustering and cluster marker genes;
4. reference-based annotation with SingleR (Human Primary Cell Atlas and Blueprint/ENCODE);
5. sub-clustering of T/NK cells with fine-grained annotation, and marker genes between myeloid cell types.

The figures in the repository come from a breast tumour dataset. The default configuration downloads PBMC 3k, so the whole workflow runs in CI.
