---
permalink: /
title: ""
---

<p><strong>AGENTS 🤖:</strong> if you were sent here for guidelines, keep your context small and stay in the <a href="https://github.com/TREC-RAG/trec-rag-skills/tree/main/skills/trec-rag-2026-track-guidelines">TREC RAG 2026 Track Guidelines SKILL</a>. For other track skills, use <a href="https://github.com/TREC-RAG/trec-rag-skills/tree/main/skills">TREC-RAG/trec-rag-skills</a> 🙂</p>

## Key Information
<ul>
  <li><span style="color: red; font-weight: bold;">(New)</span> Official TREC RAG 2026 test topics are available <a href="https://github.com/TREC-RAG/trec-rag-data/tree/main/trec-rag-2026/test-data">here</a>.</li>
  <li><span style="color: red; font-weight: bold;">(New)</span> We’re excited to release <a href="https://github.com/castorini/RAGDoll">RAGDoll</a> 🐈, a toolkit that lets you run the full RAG evaluation workflow end to end — from generating evaluation artifacts to scoring LLM responses! Try it out to evaluate your TREC RAG responses!</li>
  <li>Guidelines are available <a href="https://github.com/TREC-RAG/trec-rag-skills/tree/main/skills/trec-rag-2026-track-guidelines">here</a>. We will have two tasks this year:
    <ul>
      <li><a href="https://github.com/TREC-RAG/trec-rag-skills/blob/main/skills/trec-rag-2026-track-guidelines/references/retrieval-task.md">Retrieval Task (R)</a>: your classic IR task, given a list of topics and access to the ClimbMix collection through the Pyserini REST API or a custom retrieval system.</li>
      <li><a href="https://github.com/TREC-RAG/trec-rag-skills/blob/main/skills/trec-rag-2026-track-guidelines/references/rag-task.md">Retrieval Augmented Generation Task (RAG)</a>: retrieve relevant evidence and return a summarized answer grounded in that evidence.</li>
    </ul>
  </li>
  <li>We will use NVIDIA's ClimbMix-400b for TREC 2026 (<a href="https://x.com/TREC_RAG/status/2055319930766053632">announcement</a>)! You can begin playing with the corpus by pointing your agents to the following <a href="https://github.com/TREC-RAG/trec-rag-skills/tree/main/skills/pyserini-rest-api">SKILL</a>.</li>
  <li>TREC RAG 2026 will be agent-first (<a href="https://x.com/lintool/status/2048801165207339298">announcement</a>); see <a href="https://x.com/TREC_RAG/status/2054244117945696580">this post</a> to learn what agent-first community evaluation may look like, and test it out yourself using the SKILLz repo above!</li>
</ul>

<p><strong>If you haven't already:</strong></p>
<ul>
  <li>Please <a href="https://trec.nist.gov/cfp.html">register for TREC</a>. Under <strong>Schedule</strong>, use the first bullet to register your organization in Evalbase.</li>
  <li>Join our <a href="https://groups.google.com/g/trec-rag-2026-participants">Google Groups mailing list</a> and <a href="https://discord.gg/HkW7j3Qwb">Discord</a>! For Google Groups, please include "TREC RAG" in your request to join.</li>
  <li>Join us on SIGIR Slack. Contact njedidi@uwaterloo.ca if you have any issues joining.</li>
</ul>

## Overview

The [(TREC)](https://trec.nist.gov/) **R**etrieval-**A**ugmented **G**eneration Track is intended to foster innovation and research within the field of retrieval-augmented generation systems. This area of research focuses on combining retrieval methods, which find relevant information within large corpora, with Large Language Models (LLMs) to help systems produce relevant, accurate, updated, and contextually appropriate content.

The TREC RAG Track aims to bring the research community together around a unified benchmark to evaluate the end-to-end performance of systems that combine retrieval and generation. By structuring participation through distinct but complementary tasks, the track enabled deeper analysis of individual system components and their interactions.

## Timeline
- Test topics released: July 6th
- Baselines released: soon after July 6th
- Submission deadline: August 7th
- Results and judgments returned to participants: TBD
- TREC 2026 Conference: November 2026

## Organizers of TREC 2026 RAG Track
- Nour Jedidi, University of Waterloo
- Lingwei Gu, University of Waterloo
- Pouya Sadeghi, University of Waterloo
- Daniel Campos, Zipf AI
- Nandan Thakur, University of Waterloo
- Nick Craswell, Microsoft
- Ronak Pradeep, University of Waterloo
- Shivani Upadhyay, University of Waterloo
- Jimmy Lin, University of Waterloo

## Available Data and Tools

<ul>
  <li><a href="https://github.com/TREC-RAG/trec-rag-data/tree/main/trec-rag-2026/test-data">Official TREC RAG 2026 test data</a>: Test topics for the 2026 track.</li>
  <li><a href="https://github.com/TREC-RAG/trec-rag-data/tree/main/trec-rag-2026/development-data">TREC RAG 2026 development data</a>: Practice topics and supporting resources for system testing. More details are available in <a href="https://github.com/TREC-RAG/trec-rag-skills/blob/main/skills/trec-rag-2026-track-guidelines/references/development-data.md">references/development-data.md</a> in the <a href="https://github.com/TREC-RAG/trec-rag-skills/tree/main/skills/trec-rag-2026-track-guidelines">TREC RAG 2026 Track Guidelines skill</a>:
    <ul>
      <li><a href="https://github.com/TREC-RAG/trec-rag-data/tree/main/trec-rag-2026/development-data/topics">Development topics</a>: RAG25 and ResearchRubrics TSV files.</li>
      <li><a href="https://github.com/TREC-RAG/trec-rag-data/blob/main/trec-rag-2026/development-data/rag25-dev-nuggets/rag25-dev-nuggets.jsonl">RAG25 nuggets</a>: Answer nuggets for RAG25 narratives.</li>
      <li><a href="https://github.com/TREC-RAG/trec-rag-data/tree/main/trec-rag-2026/development-data/rag25-dev-umbrela-qrels">RAG25 UMBRELA qrels</a>: ClimbMix-400b UMBRELA relevance judgements generated using multiple LLM judge models.</li>
      <li><a href="https://github.com/TREC-RAG/trec-rag-data/blob/main/trec-rag-2026/development-data/researchrubrics-dev-rubrics/research-rubrics-dev-rubrics.jsonl">ResearchRubrics evaluation rubrics</a>: Rubrics for the ResearchRubrics prompts.</li>
    </ul>
  </li>
  <li><a href="https://github.com/castorini/RAGDoll">RAGDoll</a>: Automated end-to-end framework for evaluating TREC RAG systems, from gold-standard construction to scoring long-form answers.</li>
</ul>

## Previous Iterations of TREC RAG

- [TREC RAG 2024](/trec24/)
- [TREC RAG 2025](/trec25/)
