---
permalink: /about/
title: "What is TREC RAG?"
---

Our white paper will be released soon!

The [(TREC)](https://trec.nist.gov/) **R**etrieval-**A**ugmented **G**eneration Track is intended to foster innovation and research within the field of retrieval-augmented generation systems. This area of research focuses on combining retrieval methods - techniques for finding relevant information within large corpora with Large Language Models (LLMs) to enhance the ability of systems to produce relevant, accurate, updated and contextually appropriate content.

## 2024 Tasks Overview

We are conducting three tasks in TREC 2024 RAG track. These tasks are as follows:

1. **(R) Retrieval Task** : The “R” track requires participants to rank and retrieve the topmost relevant segments from the MS MARCO Segment v2.1 collection for the provided set of input topics, i.e., queries.

2. **(AG) Augmented Generation Task** : The "AG" track requires participants to generate RAG answers with attributions for supporting segments from the MS MARCO Segment v2.1 collection. Participants would need to use the top-k relevant segments provided by our baseline retrieval system.

3. **(RAG) Retrieval-Augmented Task** : The "RAG" track requires participants to generate RAG answers with attributions for supporting segments from the MS MARCO Segment v2.1 collection. Participants are free to choose their own retrieval system and chunking technique. We only require the participants to map their chunk to MS MARCO Segment v2.1 for reprodubicility and ease of evaluation.


## Proposed Evaluation Methodology - Version 0.1

The proposed evaluation methodology for the TREC 2024 RAG track is as follows:

![Gather Answers](/assets/images/eval-step1.png){: .align-center}
<figcaption>Given a set of queries, the participants will be asked to generate a set of answers. The answers can be generated using any method, including but not limited to retrieval, generation, or a combination of both. </figcaption>


![Evaluate Attribution](/assets/images/eval-step2.png){: .align-center}
<figcaption>Each answer will first be evaluated for how well the citations support the sentences. The set of metrics that will be released soon with the track guidelines.</figcaption>


![Pooling & Nuggetization](/assets/images/eval-step3.png){: .align-center}
<figcaption>The set of retrieved sentences will be pooled and nuggetized. More details will be added shortly.</figcaption>


![Nugget Assignment](/assets/images/eval-step4.png){: .align-center}
<figcaption>We go over all nuggets and assign them to each sentence in a participant answer. Note, we can have multiple nuggets assigned to a single sentence.</figcaption>{: .text-center}


![Score Aggregation](/assets/images/eval-step5.png){: .align-center}
<figcaption>We aggregate scores from the prior steps along with additional linguistic features like fluency, coherence, etc. to generate a final score for each answer.</figcaption>

## Timeline

```
Development Topics and baselines released: Week 1, June 2024
Final Topics released: August 4th, 2024
Submission deadline: August 11th, 2024
Results and judgments (whatever form it takes) returned to participants: October 2024
TREC 2024 Conference: November 2024
```

## Organizers of TREC 2024 RAG Track

- Ronak Pradeep, University of Waterloo
- Nandan Thakur, University of Waterloo
- Jimmy Lin, University of Waterloo
- Nick Craswell, Microsoft