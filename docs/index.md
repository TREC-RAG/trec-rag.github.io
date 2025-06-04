---
permalink: /
title: "What is TREC RAG?"
---

## Overview

The [(TREC)](https://trec.nist.gov/) **R**etrieval-**A**ugmented **G**eneration Track is intended to foster innovation and research within the field of retrieval-augmented generation systems. This area of research focuses on combining retrieval methods - techniques for finding relevant information within large corpora with Large Language Models (LLMs) to enhance the ability of systems to produce relevant, accurate, updated and contextually appropriate content.

The TREC 2024 RAG Track consisted of three tasks designed to evaluate various aspects of retrieval-augmented generation systems using the MS MARCO Segment v2.1 collection. The Retrieval (R) Task involved ranking and retrieving the most relevant text segments for a given set of queries. The Augmented Generation (AG) Task required participants to generate answers with attributions to supporting segments, using a fixed set of top-k segments provided by a baseline retrieval system. The Retrieval-Augmented Generation (RAG) Task allowed participants to use their own retrieval and chunking strategies, provided that their outputs were mapped to the MS MARCO Segment v2.1 collection to ensure reproducibility and facilitate evaluation.

The TREC RAG Track aims to bring the research community together around a unified benchmark to evaluate the end-to-end performance of systems that combine retrieval and generation. By structuring participation through distinct but complementary tasks, the track enabled deeper analysis of individual system components and their interactions.

## 2025 Tasks Outline

We are conducting three tasks in TREC 2025 RAG track. These tasks are as follows:

1. **(R) Retrieval Task** : The "R" track requires participants to rank and retrieve the most relevant segments from the MS MARCO Segment v2.1 collection based on a given set of input topics (queries).

2. **(AG) Augmented Generation Task** : The "AG" track requires participants to generate RAG answers, including attributions to supporting segments from the MS MARCO Segment v2.1 collection. Participants would need to use the top-k relevant segments provided by our baseline retrieval system.

3. **(RAG) Retrieval-Augmented Task** : The "RAG" track requires participants to generate RAG answers along with attributions for supporting segments from the MS MARCO Segment v2.1 collection. Participants can choose their own retrieval system and chunking technique. We only require the participants to map their chunk to MS MARCO Segment v2.1 for reprodubicility and ease of evaluation.

Details on how to submit your runs will be shared shortly.

## Announcements

The TREC 2025 RAG Corpus details are available [here](https://trec-rag.github.io/annoucements/2025-rag25-corpus/).

Stay tuned for more information for the TREC RAG 2025 Track!

## Organizers of TREC 2025 RAG Track

- Shivani Upadhyay, University of Waterloo
- Ronak Pradeep, University of Waterloo
- Nandan Thakur, University of Waterloo
- Jimmy Lin, University of Waterloo
- Nick Craswell, Microsoft

## Explore More RAG Tracks at TREC 2025

Please check out the following tracks that also support RAG-based approaches — cross-participation is encouraged!


[TREC BioGEN 2025 Track](https://trec-biogen.github.io/docs/)

[TREC DRAGUN 2025 Track](https://trec-dragun.github.io/)

[TREC IKAT 2025 Track](https://www.trecikat.com)

[TREC RAGTIME 2025 Track](https://trec-ragtime.github.io/)