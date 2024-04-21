---
title: "TREC 2024 RAG Corpus"
date: 2024-04-18T08:00:00-00:00
categories:
 - Annoucements
tags:
 - TREC 2024
 - Corpus
classes: wide
toc: false
---

We are happy to introduce the MS MARCO V2.1 document corpus and its *segmented version* for this year's TREC RAG Track!

## MS MARCO V2.1 Document Corpus
The MS MARCO V2.1 document corpus has been cleaned following some deduping from the MS MARCO V2 document corpus. Our initial plan was to utilize the MS MARCO V2 passage corpus. However, Community feedback ([Twitter post](https://twitter.com/TREC_RAG/status/1772324651659636781)) and discussions with Jeff Dalton influenced us to reconsider our option. A notable concern with the original corpus (MS MARCO V2) was the presence of duplicate passages, making evaluation harder (more holes, inconsistencies, etc.). Additionally, with passages, important considerations like length, chunking, etc. are not explored while they could be important to both researchers and practitioners. Note that for the filtered corpus, we applied an additional `body = body.strip()` step to allow for *precise* `start_char` and `end_char` calculation such that we could match the segments from the MS MARCO V2 corpus exactly (these fields are missing in the V2 corpus). The other fields have not been changed from the MS MARCO V2 document corpus except the document identifier which we modified to keep the original meaning (JSONL file and start position byte offset, more on this later). The new corpus has 10,960,555 documents compared to the original which had 11,959,635 documents. 

### Document Format
Each MS MARCO V2.1 document has five fields: 
 - `docid` which contains the unique document identifier
 - `url` of the MS MARCO V2.1 document
 - `title` which denotes the title of the MS MARCO V2.1 document
 - `headings` which contains each subheading of the MS MARCO V2.1 document
 - `body` contains the body text of the MS MARCO V2.1 document

### Example
Below is an example of a document from the MS MARCO V2.1 document corpus:

```python
{
 'docid': 'msmarco_v2.1_doc_29_677149',
 'url': 'https://studyelectrical.com/2019/07/aeolian-vibration-of-transmission-conductors.html', 
 'title': 'Aeolian Vibration of Transmission Conductors', 
 'headings': 'Aeolian Vibration of Transmission Conductors\nAeolian Vibration of Transmission Conductors\nWhat is Aeolian Vibration?\nWind causes a variety of motions on transmission line conductors. Important among them are\nHow Aeolian Vibration Occurs?\nTheory/Mechanism of Aeolian Vibration\nFactors Affecting Aeolian Vibration\nEffects of Aeolian Vibration\nAeolian Vibration Damping Devices\n', 
 'body': "Aeolian Vibration of Transmission Conductors\nAeolian Vibration of Transmission Conductors\nCategories Uncategorized\nTable of Contents\nWhat is Aeolian Vibration?\nHow Aeolian Vibration Occurs?\nTheory/Mechanism of Aeolian Vibration\nFactors Affecting Aeolian Vibration\nEffects of Aeolian Vibration [...] These motions are generally characterized as low frequency and high amplitude. If these motions are not controlled, they can produce damage to the conductor and other elements in the transmission system.\nAeolian vibration, on the other hand, is associated with smooth non-turbulent winds in the range of 2 MPH (miles per hour) to 15 MPH and can occur on a daily basis. Aeolian vibration is characterized by high frequency and low amplitude motion.\nThis article describes the theory and mechanism of aeolian vibration, effects of aeolian vibration and different dampers used to reduce the harmfull effect of aeolian vibration.\nHow Aeolian Vibration Occurs?\nAeolian vibrations occur when a smooth wind flow of 2 to 15 mph (1 to 7 m/s) interacts a conductor.\nWhen this happens, air accelerates to go around the conductor and then separates behind it as seen in Figure below.\nVortex formation and Aeolian Vibration occurring in a Transmission Line\nThis motion creates a low-pressure region at the opposite side of the conductor and the air shows a tendency to move\ninto this vacuum zone. This is the vortex shedding action that creates an alternating pressure imbalance causing the conductor to move up and down at a ninety-degree angle to the flow direction. [...] Spring-piston dampers, pneumatic dampers, and Stockbridge dampers are classified as the tuned dampers which are effective when their natural frequency coincide with the excitation frequency of the conductor.\nUnlike the spring-piston dampers and the pneumatic dampers, the Stockbridge dampers can be tuned to be effective over a wide range of frequency and they can dissipate vibrations in any directions.\nTesla is an Electrical Engineer, Physicist and an Inventor in making. He is a good writer and author of many courses and articles published in this site."
}
```

Consider the document above, the `docid` `msmarco_v2.1_doc_29_677149` encodes the filename and starting position of the document's jsonl line. So `_29` and `_677149` indicates the document is in the file `msmarco_v2_doc/msmarco_doc_29` at *byte* offset 677149. 


## MS MARCO V2.1 Document Corpus - Segmented Version
We also provide the community with a segmented version of the MS MARCO V2.1 document corpus. The segmented version of V2.1 has two new fields `start_char` and `end_char` containing the start and end position of the segment in the body of the corresponding MS MARCO V2.1 document. To get this corpus, we first reproduced the original segmentation from the MS MARCO V2 document corpus, involving steps like finding the precise `spacy` version. The resultant process leverages a sliding window size of 10 sentences and a stride of 5 sentences to create segments of text, roughly between 500-1000 characters, making it more manageable for users and baselines. We plan to leverage this resultant segmented MS MARCO V2.1 document corpus heavily in the TREC 2024 RAG Track, more in the upcoming task description. The corpus contains 113,520,750 segments in total. 


### Segment Format
Each MS MARCO V2.1 segment has seven fields: 
 - `docid` which contains the unique segment identifier
 - `url` of the segment from MS MARCO V2.1 document
 - `title` which denotes the title of the MS MARCO V2.1 document
 - `headings` which contains each subheading of the MS MARCO V2.1 document
 - `segment` contains the chunked text
 - `start_char` contains the start position character of the segment in the corresponding MS MARCO V2.1 document
 - `end_char` contains the end position character of the segment in the corresponding MS MARCO V2.1 document

### Example
Below is an example of a segment from the segmented MS MARCO V2.1 document corpus:

```python
{
 'docid': 'msmarco_v2.1_doc_29_677149#3_1637632', 
 'url': 'https://studyelectrical.com/2019/07/aeolian-vibration-of-transmission-conductors.html', 
 'title': 'Aeolian Vibration of Transmission Conductors', 
 'headings': 'Aeolian Vibration of Transmission Conductors\nAeolian Vibration of Transmission Conductors\nWhat is Aeolian Vibration?\nWind causes a variety of motions on transmission line conductors. Important among them are\nHow Aeolian Vibration Occurs?\nTheory/Mechanism of Aeolian Vibration\nFactors Affecting Aeolian Vibration\nEffects of Aeolian Vibration\nAeolian Vibration Damping Devices\n', 
 'segment': 'These motions are generally characterized as low frequency and high amplitude. If these motions are not controlled, they can produce damage to the conductor and other elements in the transmission system. Aeolian vibration, on the other hand, is associated with smooth non-turbulent winds in the range of 2 MPH (miles per hour) to 15 MPH and can occur on a daily basis. Aeolian vibration is characterized by high frequency and low amplitude motion. This article describes the theory and mechanism of aeolian vibration, effects of aeolian vibration and different dampers used to reduce the harmfull effect of aeolian vibration. How Aeolian Vibration Occurs? Aeolian vibrations occur when a smooth wind flow of 2 to 15 mph (1 to 7 m/s) interacts a conductor. When this happens, air accelerates to go around the conductor and then separates behind it as seen in Figure below. Vortex formation and Aeolian Vibration occurring in a Transmission Line\nThis motion creates a low-pressure region at the opposite side of the conductor and the air shows a tendency to move\ninto this vacuum zone. This is the vortex shedding action that creates an alternating pressure imbalance causing the conductor to move up and down at a ninety-degree angle to the flow direction.', 
 'start_char': 1806, 
 'end_char': 3061
},
```

Consider the segment above, the `docid` `msmarco_v2.1_doc_29_677149#3_1637632` encodes the filename and starting position of the corresponding document's jsonl line, the segment number of the document (0-indexed), and the starting position of the segment's jsonl line (filename is the same as that of the document). So `_29` and `_677149` indicate the corresponding document is in the file `msmarco_v2_doc/msmarco_doc_29` at *byte* offset 677149. The `#3_1637632` indicates the segment is the 4th segment for the document `msmarco_v2.1_doc_29_677149` and you can find the segment in the file `msmarco_v2_doc_segmented/msmarco_doc_segmented_29` at *byte* offset 1637632.

## Deduplication Specifics
To avoid issues stemming from duplicate documents plaguing the MS MARCO V2 document corpus, we adopted deduplication. The initial step involved a selection of duplicates and an establishment of equivalence classes of documents, run by Ian Soboroff from NIST, and used an LSH with minhash and 9-gram shingles. Our deduplication process involved selecting a representative `DocID` for each equivalence class. Utilizing these DocIDs, we refined our MS MARCO V2 Document collection—both its original and segmented versions—to generate two new corpora. The resultant stats are summarized below:

| Collection | Version 2.0 (Original) | Version 2.1 (Ours) |
| :--------: | :---------------------: | :----------------: |
| MS MARCO Document Corpus | 11,959,635 | 10,960,555 |
| MS MARCO Document Corpus - Segmented | 124,131,414 | 113,520,750 |


## Modified relevance judgments for TREC DL 2021-2023 and Dev/Dev2 sets

We additionally map the relevance judgments from the TREC DL 2021-2023 and Dev/Dev2 sets from the original collection to the MS MARCO V2.1 document corpus. This will allow the community to better leverage the MS MARCO V2.1 document collection to test their retrieval and ranking models.

## Where can I find the corpus?

The MS MARCO V2.1 document corpus and its segmented version are available to download courtesy of Microsoft! You can find the details below:

| Collection | Filename | File size | Num Records | Format | MD5 Checksum |
| :----------------: | :---------------------: | :----------------: | :----------------: | :----------------: | :----------------: |
| MS MARCO V2.1 Document Corpus | [msmarco_v2.1_doc.tar](https://msmarco.z22.web.core.windows.net/msmarcoranking/msmarco_v2.1_doc.tar) | 28.1 GB | 10,960,555 | tar of 70 gzipped jsonl files | `a5950665d6448d3dbaf7135645f1e074` |
| MS MARCO V2.1 Document Corpus - Segmented | [msmarco_v2.1_doc_segmented.tar](https://msmarco.z22.web.core.windows.net/msmarcoranking/msmarco_v2.1_doc_segmented.tar) | 25.1 GB | 113,520,750 | tar of 70 gzipped jsonl files | `3799e7611efffd8daeb257e9ccca4d60` |

## And the updated qrels?

The updated qrels for the TREC DL 2021-2023 and Dev/Dev2 sets are available to download via Anserini! You can find the details below:

| Set | Filename | Num Records | Format | MD5 Checksum |
| :--------: | :---------------------: | :----------------: | :----------------: | :----------------: |
| TREC DL 2021 | [qrels.dl21-doc-msmarco-v2.1.txt](https://raw.githubusercontent.com/castorini/anserini-tools/master/topics-and-qrels/qrels.dl21-doc-msmarco-v2.1.txt) | 10,973 | TREC qrels format | `6845b6c128aec71027e72078a960600e` |
| TREC DL 2022 | [qrels.dl22-doc-msmarco-v2.1.txt](https://raw.githubusercontent.com/castorini/anserini-tools/master/topics-and-qrels/qrels.dl22-doc-msmarco-v2.1.txt) | 349,541 | TREC qrels format | `ac9f5c6fcb6972d8bf13b07ab150680a` |
| TREC DL 2023 | [qrels.dl23-doc-msmarco-v2.1.txt](https://raw.githubusercontent.com/castorini/anserini-tools/master/topics-and-qrels/qrels.dl23-doc-msmarco-v2.1.txt) | 15,995 | TREC qrels format | `4b30e8850b6fba56289b6c177afe959b` |
| MS MARCO Dev | [qrels.msmarco-v2.1-doc.dev.txt](https://raw.githubusercontent.com/castorini/anserini-tools/master/topics-and-qrels/qrels.msmarco-v2.1-doc.dev.txt) | 4,702 | TREC qrels format | `089b19dce0a6f74d3f01fd988d439f2f` |
| MS MARCO Dev2 | [qrels.msmarco-v2.1-doc.dev2.txt](https://raw.githubusercontent.com/castorini/anserini-tools/master/topics-and-qrels/qrels.msmarco-v2.1-doc.dev2.txt) | 5,177 | TREC qrels format | `8ff337f2110ea44ba8c5533a7eff6222` |

Topics corresponding to the TREC DL 2021-2023 and Dev/Dev2 sets are the same as the original sets, but for convenience you can also find them here:


| Set | Filename | Num Records | Format | MD5 Checksum |
| :--------: | :---------------------: | :----------------: | :----------------: | :----------------: |
| TREC DL 2021 | [topics.dl21.txt](https://raw.githubusercontent.com/castorini/anserini-tools/master/topics-and-qrels/topics.dl21.txt) | 477 | TREC topics format | `46d863434dda18300f5af33ee29c4b28` |
| TREC DL 2022 | [topics.dl22.txt](https://raw.githubusercontent.com/castorini/anserini-tools/master/topics-and-qrels/topics.dl22.txt) | 500 | TREC topics format | `f1bfd53d80e81e58207ce557fd2211a0` |
| TREC DL 2023 | [topics.dl23.txt](https://raw.githubusercontent.com/castorini/anserini-tools/master/topics-and-qrels/topics.dl23.txt) | 700 | TREC topics format | `7df9e17b47cc9aa5d1c9fd5b313e273c` |
| MS MARCO Dev | [topics.msmarco-v2-doc.dev.txt](https://raw.githubusercontent.com/castorini/anserini-tools/master/topics-and-qrels/topics.msmarco-v2-doc.dev.txt) | 4,552 | TREC topics format | `b05dc19f1d2b8ad729f189328a685aa1` |
| MS MARCO Dev2 | [topics.msmarco-v2-doc.dev2.txt](https://raw.githubusercontent.com/castorini/anserini-tools/master/topics-and-qrels/topics.msmarco-v2-doc.dev2.txt) | 5,000 | TREC topics format | `f000319f1893a7acdd60fdcae0703b95` |

## Next Steps
We have already implemented [Anserini]()/Pyserini retrieval baselines for these sets and are in the process of packaging things! Additionally, we hope to provide reranking baselines with state-of-the-art RankZephyr, RankGPT, and Cohere Rerank 3 models through [RankLLM](rankllm.ai).

More information on the topics for the TREC 2024 RAG Track will be released soon. Stay tuned!

So long and thanks for all the fish 🐟,

TREC RAG Organizers