---
title: "A small LLM for critical reading of papers"
subtitle: "QLoRA fine-tuning of TinyLlama-1.1B"
excerpt: "A LoRA adapter trained with QLoRA so TinyLlama answers reviewer-style questions about a paper and returns claims, assumptions and limitations as validated JSON."
date: 2026-02-17
author: "Sourabh Kumar"
draft: false
weight: 10
tags:
  - LLM
  - QLoRA
  - PEFT
  - NLP
  - Python
categories:
  - Machine learning
layout: single
links:
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/bioinfosourabh/qlora-scientific-reasoning
---

Can a 1.1-billion-parameter model, trained on a free Colab GPU, learn to read a study the way a reviewer does? This project fine-tunes TinyLlama-1.1B-Chat with QLoRA:

- the base model is loaded in 4-bit NF4 with double quantisation, and LoRA adapters (r = 16, α = 32) are trained on the attention projections;
- PDFs are split into overlapping 1,500-character chunks, and conversations keep three turns of history;
- in structured mode the model returns a JSON *reasoning pack* (claims, assumptions, limitations, confidence and evidence spans), which is parsed, repaired and validated against the source text;
- an evaluation reports JSON validity, field coverage, ROUGE-L, grounding, and how often the model echoes the prompt or keeps writing past its answer.

The first runs taught a practical lesson: with fewer than about 30 distinct examples, TinyLlama continues the paper text instead of answering. The repository documents those failure modes and the fixes for them.
