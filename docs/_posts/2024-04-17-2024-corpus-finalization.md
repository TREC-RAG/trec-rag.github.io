---
title: "TREC RAG 2024 Corpus Finalization"
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

# MS MARCO V2.1 Document Corpus
The MS MARCO V2.1 document corpus has been cleaned following some deduping from the MS MARCO V2 document corpus. Our initial plan was to utilize the MS MARCO V2 passage corpus. However, following some community feedback ([Twitter post](https://twitter.com/TREC_RAG/status/1772324651659636781)) and internal discussion with others like Jeff Dalton led us to reconsider our option and make this choice. A notable concern with the original corpus (MS MARCO V2) was the presence of duplicate passages, making evaluation harder. Additionally, with passages, important considerations like length, chunking, etc. are not explored while they could be important to both researchers and practitioners. Note that for the filtered corpus, we applied an additional `body = body.strip()` step to allow for *precise* `start_char` and `end_char` calculation such that we could match the segments from the MS MARCO V2 corpus exactly (these fields are missing in the V2 corpus). The new corpus has 10,960,555 documents compared to the original which had 11,959,635 documents. 

# MS MARCO V2.1 Document Corpus - Segmented Version
We also provide the community with a segmented version of the MS MARCO V2.1 document corpus. The segmented version of V2.1 has two new fields `start_char` and `end_char` containing the start and end position of the segment in the body of the corresponding MS MARCO V2.1 document. To get this corpus, we first reproduced the original segmentation from the MS MARCO V2 document corpus, involving steps like finding the precise `spacy` version. The resultant process leverages a sliding window size of 10 sentences and a stride of 5 sentences to create segments of text, roughly between 500-1000 characters. The resultant segmented MS MARCO V2.1 document corpus will be used primarily in the TREC RAG 2024 Track. The corpus contains 113,520,750 segments in total. 

> The MS MARCO segment id `msmarco_v2.1_doc_29_677149#3_1637632` contains the mapping information from which document (`msmarco_v2.1_doc_29_677149`) it has been segmented. The suffix `#3` denotes the 4th segment of the document, and `_1637632` denotes the *byte* offset of the position of the segment in the corpus file. 

Each MS MARCO V2.1 segment has seven keys: 
 - `docid` which contains the unique segment identifier
 - `url` of the segment from MS MARCO V2.1 document
 - `title` which denotes the title of the MS MARCO V2.1 document
 - `headings` which contains each subheadings of the MS MARCO V2.1 document
 - `segment` contains the chunked text
 - `start_char` contains the start position character of the segment in the corresponding MS MARCO V2.1 document
 - `end_char` contains the end position character of the segment in the corresponding MS MARCO V2.1 document

Below is an example of a segment from the segmented MS MARCO V2.1 document corpus:

```python
{
    'docid': 'msmarco_v2.1_doc_29_677149#3_1637632', 
    'url': 'https://studyelectrical.com/2019/07/aeolian-vibration-of-transmission-conductors.html', 
    'title': 'Aeolian Vibration of Transmission Conductors', 
    'headings': 'Aeolian Vibration of Transmission Conductors\nAeolian Vibration of Transmission Conductors\nWhat is Aeolian Vibration?\nWind causes a variety of motions on transmission line conductors. Important among them are\nHow Aeolian Vibration Occurs?\nTheory/Mechanism of Aeolian Vibration\nFactors Affecting Aeolian Vibration\nEffects of Aeolian Vibration\nAeolian Vibration Damping Devices\n', 
    'segment': 'These motions are generally characterized as low frequency and high amplitude. If these motions are not controlled, they can produce damage to the conductor and other elements in the transmission     system. Aeolian vibration, on the other hand, is associated with smooth non-turbulent winds in the range of 2 MPH (miles per hour) to 15 MPH and can occur on a daily basis. Aeolian vibration is characterized by high frequency and low amplitude motion. This article describes the theory and mechanism of aeolian vibration, effects of aeolian vibration and different dampers used to reduce the harmfull effect of aeolian vibration. How Aeolian Vibration Occurs? Aeolian vibrations occur when a smooth wind flow of 2 to 15 mph (1 to 7 m/s) interacts a conductor. When this happens, air accelerates to go around the conductor and then separates behind it as seen in Figure below. Vortex formation and Aeolian Vibration occurring in a Transmission Line\nThis motion creates a low-pressure region at the opposite side of the conductor and the air shows a tendency to move\ninto this vacuum zone. This is the vortex shedding action that creates an alternating pressure imbalance causing the conductor to move up and down at a ninety-degree angle to the flow direction.', 
    'start_char': 1806, 
    'end_char': 3061
},
```

### MS MARCO V2.1 Document
The MS MARCO V2.1 document corpus after deduplication contains 10,960,555 (~10.96 million) documents. The metadata has not been changed from the original MS MARCO V2 document corpus just with the exception of the document id which we have uniquely defined for each document.

> The MS MARCO document id `msmarco_v2.1_doc_29_677149`contains the document information and `_29` and `_677149` denotes the *byte* offset of the position of the document in the collection. 

Each MS MARCO V2.1 document has five keys: 
 - `docid` which contains the unique document identifier
 - `url` of the MS MARCO V2.1 document
 - `title` which denotes the title of the MS MARCO V2.1 document
 - `headings` which contains each subheadings of the MS MARCO V2.1 document
 - `body`contains the body text of the MS MARCO V2.1 document


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

### More specifics on MS MARCO V2 document deduplication
To avoid issues stemming from duplicate documents in the MS MARCO V2 document corpus, we adopted deduplication. First, involved a selection of duplicates and an establishment of equivalence classes of documents, run by Ian Soboroff from NIST following an LSH with minhash and 9-gram shingles. Our deduplication process involved selecting a representative `DocID` for each equivalence class. Utilizing these DocIDs, we refined our MS MARCO V2 Document collection—both its original and segmented versions—to generate two new collections and subsequently indexes. The resultant stats are summarized below:

| Collection |  Version 2.0 (Original) | Deduped 2.1 (Ours) |
| :--------: | :---------------------: | :----------------: |
| MS MARCO Document | 11,959,635 | 10,960,555 |
| MS MARCO Segment | 124,131,414 | 113,520,750 |