---
title: "Genomics pipelines on AWS Batch"
subtitle: "Terraform infrastructure for Nextflow in the cloud"
excerpt: "Terraform for S3, AWS Batch (Spot and On-Demand, scaling to zero), least-privilege IAM and budget alerts, with launch scripts to run Nextflow pipelines on it."
date: 2026-11-15
author: "Sourabh Kumar Daksh"
draft: false
weight: 11
tags:
  - AWS
  - Terraform
  - Nextflow
  - cloud
categories:
  - Pipelines
layout: single
links:
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/bioinfosourabh/AWS-Genomics-Workflow
---

Infrastructure as code for running Nextflow genomics pipelines on AWS Batch:

- an S3 work bucket with expiry rules, and read-only access to input and reference buckets;
- Spot and On-Demand Batch compute environments that scale to zero when idle;
- least-privilege IAM roles, a launch template with a larger disk for genomics jobs, and a budget alert;
- a generated Nextflow configuration and launch scripts, including running the Nextflow head job itself on Batch.

The worked example runs the [germline/somatic pipeline](/project/ngs-automation-nextflow/) on FASTQ files in S3; the same setup serves the other pipelines here and nf-core workflows.
