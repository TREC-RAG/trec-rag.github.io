---
title: "TREC 2024 RAG UMBRELA Qrels Released"
date: 2024-11-17T12:00:00-00:00
categories:
  - Annoucements
tags:
  - TREC 2024
  - Qrels
classes: wide
toc: false
---

We have just released relevance judgments using UMBRELA [1] for the 301 RAG test topics which we used for our evaluations [2]. You can find them at:
- RAG 2024 UMBRELA qrels: [qrels.rag24.test-umbrela-all.txt](/assets/txt/qrels.rag24.test-umbrela-all.txt)

RAG 2024 Topics: [topics.rag24.test.txt](/assets/txt/topics.rag24.test.txt)

Command used with `trec_eval` (version: 9.0.4):
```
trec_eval -c -m recall.100 qrels.rag24.test-umbrela-all.txt <result_file>
trec_eval -c -m ndcg_cut.100 qrels.rag24.test-umbrela-all.txt <result_file>
trec_eval -q -c -m ndcg_cut.20 qrels.rag24.test-umbrela-all.txt <result_file>
```

[1] Upadhyay et al. "UMBRELA: UMbrela is the (Open-Source Reproduction of the) Bing RELevance Assessor." [https://arxiv.org/abs/2406.06519](https://arxiv.org/abs/2406.06519).

[2] Upadhyay et al. "A Large-Scale Study of Relevance Assessments with Large Language Models: An Initial Look." [https://arxiv.org/abs/2411.08275](https://arxiv.org/abs/2411.08275).

Regards,
The TREC 2024 RAG Organizers
