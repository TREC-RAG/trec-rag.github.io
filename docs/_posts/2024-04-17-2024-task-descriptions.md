---
title: "TREC RAG 2024 Corpus & Task Description"
date: 2024-04-17T08:00:00-00:00
categories:
  - Annoucements
tags:
  - TREC 2024
  - Corpus
  - Tasks
classes: wide
toc: false
---

We provide details on our corpus selection and task descripts for the TREC RAG 2024 track.

## TREC RAG Corpus Description
We are happy to introduce the MS MARCO v2.1 document and segment collection for this year's TREC-RAG challenge!

### Introduction
The MS MARCO v2.1 document and segment collection has been cleaned and deduped from the MSMARCOv2 document collection. Our initial plan was to utilize the MS MARCO v2 Passage Collection. However, community feedback ([Twitter post](https://twitter.com/TREC_RAG/status/1772324651659636781)) led us to reconsider our option and select the MS MARCO v2 Document collection. A notable concern with this passage collection was the presence of duplicate passages.

### MS MARCO v2.1 Segment
We implement a sliding window-based filtering to segment each MSMARCO v2.1 document into chunks of segments of text containing anywhere between 500-1000 characters. The MS MARCO v2.1 segment collection would be used in the TREC-RAG 2024 task. The MS MARCO v2.1 segment collection after deduplication contains 113,520,750 segments in total. 

> The MS MARCO segment id `msmarco_v2.1_doc_29_677149#3_1637632`contains the mapping information from which document (`msmarco_v2.1_doc_29_677149`) it has been segmented. The suffix `#3` denotes the 3rd segment of the document, and `_1637632` denotes the *byte* offset of the position of the segment in the collection. 

Each MS MARCO v2.1 segment has seven keys: 
 - `docid` which contains the unique segment identifier
 - `url` of the segment from MS MARCO v2.1 document
 - `title` which denotes the title of the MS MARCO v2.1 document
 - `headings` which contains each subheadings of the MS MARCO v2.1 document
 - `segment`contains the chunked text
 - `start_char` contains the start position character of the segment in MS MARCO v2.1 document
 - `end_char` contains the end position character of the segment in MS MARCO v2.1 document

Below is an example of a segment from the MS MARCO v2.1 segment collection:

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

### MS MARCO v2.1 Document
The MS MARCO v2.1 document collection after deduplication contains 10,960,555 (~10.96 million) documents. The metadata has not been changed from the original MS MARCO v2 document collection just with the exception of the document id which we have uniquely defined for each document.

> The MS MARCO document id `msmarco_v2.1_doc_29_677149`contains the document information and `_29` and `_677149` denotes the *byte* offset of the position of the document in the collection. 

Each MS MARCO v2.1 document has five keys: 
 - `docid` which contains the unique document identifier
 - `url` of the MS MARCO v2.1 document
 - `title` which denotes the title of the MS MARCO v2.1 document
 - `headings` which contains each subheadings of the MS MARCO v2.1 document
 - `body`contains the body text of the MS MARCO v2.1 document


Below is an example of a document from the MS MARCO v2.1 document collection:

```python
{
    'docid': 'msmarco_v2.1_doc_29_677149',
    'url': 'https://studyelectrical.com/2019/07/aeolian-vibration-of-transmission-conductors.html', 
    'title': 'Aeolian Vibration of Transmission Conductors', 
    'headings': 'Aeolian Vibration of Transmission Conductors\nAeolian Vibration of Transmission Conductors\nWhat is Aeolian Vibration?\nWind causes a variety of motions on transmission line conductors. Important among them are\nHow Aeolian Vibration Occurs?\nTheory/Mechanism of Aeolian Vibration\nFactors Affecting Aeolian Vibration\nEffects of Aeolian Vibration\nAeolian Vibration Damping Devices\n', 
    'body': "Aeolian Vibration of Transmission Conductors\nAeolian Vibration of Transmission Conductors\nCategories Uncategorized\nTable of Contents\nWhat is Aeolian Vibration?\nHow Aeolian Vibration Occurs?\nTheory/Mechanism of Aeolian Vibration\nFactors Affecting Aeolian Vibration\nEffects of Aeolian Vibration [...] These motions are generally characterized as low frequency and high amplitude. If these motions are not controlled, they can produce damage to the conductor and other elements in the transmission system.\nAeolian vibration, on the other hand, is associated with smooth non-turbulent winds in the range of 2 MPH (miles per hour) to 15 MPH and can occur on a daily basis. Aeolian vibration is characterized by high frequency and low amplitude motion.\nThis article describes the theory and mechanism of aeolian vibration, effects of aeolian vibration and different dampers used to reduce the harmfull effect of aeolian vibration.\nHow Aeolian Vibration Occurs?\nAeolian vibrations occur when a smooth wind flow of 2 to 15 mph (1 to 7 m/s) interacts a conductor.\nWhen this happens, air accelerates to go around the conductor and then separates behind it as seen in Figure below.\nVortex formation and Aeolian Vibration occurring in a Transmission Line\nThis motion creates a low-pressure region at the opposite side of the conductor and the air shows a tendency to move\ninto this vacuum zone. This is the vortex shedding action that creates an alternating pressure imbalance causing the conductor to move up and down at a ninety-degree angle to the flow direction. [...] Spring-piston dampers, pneumatic dampers, and Stockbridge dampers are classified as the tuned dampers which are effective when their natural frequency coincide with the excitation frequency of the conductor.\nUnlike the spring-piston dampers and the pneumatic dampers, the Stockbridge dampers can be tuned to be effective over a wide range of frequency and they can dissipate vibrations in any directions.\nTesla is an Electrical Engineer, Physicist and an Inventor in making. He is a good writer and author of many courses and articles published in this site."
}
```

### MS MARCO v2 document deduplication
To avoid the duplicate document issue in MSMARCOv2 document collection, we adopted a deduplication strategy involving a LSH + minhash algorithm. Our deduplication process involved selecting a representative `docID` for each equivalence class. Utilizing these DocIDs, we refined our MS MARCO v2 Document collection—both its original and segmented versions—to generate two new collections and subsequently indexes. The effect on the index size was significant:

| Collection |  Version 2.0 (Original) | Deduped 2.1 (Ours) |
| :--------: | :---------------------: | :----------------: |
| MS MARCO Document | 11,959,635 | 10,960,555 |
| MS MARCO Segment | 124,131,414 | 113,520,750 |

# TREC-RAG Task Description

We are conducting three tasks in TREC-RAG 2024 competition. These are named as follows:
- [1] **(R)** Retrieval Track
- [2] **(AG)** Augmented Generation Track
- [3] **(RAG)** Retrieval-Augmented Generation Track

Below we provide details on each task which will be conducted in the first version of the TREC-RAG 2024.

## TASK 1: Retrieval Track (R)

- **Given**: Participants will be provided a list of topics and the complete MSMARCO v2.1 segment collection.
- **Task**: Provide back the run file containing the top relevant segments from the MSMARCO v2.1 segment collection for each individual topic. 
- **Notes**: The “R” track emulates the previous TREC-DL 2022/2023 tracks is for the IR audience, however, the main difference lies in using document segments from the MSMARCO v2.1 segment collection instead of the MSMARCO v2.0 passage collection.

### Inputs to user

1. List of queries as topics as TSV: <`trec_rag_queries.tsv`>

```bash
# Example of `trec_rag_queries.tsv`
...
2027497	how often should you take your toddler to the potty when potty training
300986	how many years in jail for money laundering
835760	what is the name of the triangular region at the base of the bladder?
...
```

2. MSMARCOv2.1 segment corpus as JSONL: <`msmarco_v2.1_doc_segmented_XX.json.gz`>

```python
# Example of `msmarco_v2.1_doc_segmented_XX.json.gz`
...
{
    "docid": "msmarco_v2.1_doc_51_822664157#2", 
    "url": "https://www.romper.com/p/how-often-should-i-take-my-toddler-to-the-potty-there-are-some-guidelines-to-follow-71586", 
    "title": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "headings": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nHow Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "segment": "Self-esteem can be fragile at this time, so it's important to toilet train gently, letting your child lead the way. Additionally, it's unwise to begin potty training unless your child is truly ready. Take this potty training readiness quiz featured in Parents before you begin. Elizabeth Pantley, author of The No-Cry Potty Training Solution, explained in an excerpt on Child Development Info that most toddlers pee four to eight times per day. On top of that, toddlers have one or two bowel movements a day. But every toddler is an individual. Some will go more often than that, and others will last a couple days without having a bowel movement at all. In terms of actually getting your toddler to the potty, Pantley suggested setting up a potty routine. Potty first thing in the morning, after eating, and before other activities, like riding in the car or going to sleep. Of course, you can adapt this routine to your lifestyle, and you still must be on the lookout for signs your toddler has to go ahead of schedule.", 
    "start_char": 1445, 
    "end_char": 2466
},
{
    "docid": "msmarco_v2.1_doc_28_505998624#22", 
    "url": "https://sleepingshouldbeeasy.com/potty-training-accidents/", 
    "title": "Potty Trained Toddler Having Accidents on Purpose?", 
    "headings": "Secrets to Fixing Your Toddler’s Potty Training Accidents\nSecrets to Fixing Your Toddler’s Potty Training Accidents\nTable of Contents\nHow to handle a potty trained toddler having accidents on purpose\nWhy potty training accidents happen\n1. Stop the rewards\nLearn more about why rewards don’t always work.\n2. Don’t label your child in negative ways\nLearn more about the downsides of labeling our kids.\n3. Go back to the drawing board\nLearn what to do when your toddler won’t poop on the potty.\n4. Watch your reaction\nGet tips on what to do when your 4 year old won’t poop on potty.\n5. Take your child to the potty frequently\nGet more tips on how to ease your child’s potty training poop anxiety.\n6. Practice good potty training habits\nLearn why you shouldn’t worry when your toddler refuses to sit on potty.\nConclusion\n", 
    "segment": "Get tips on what to do when your 4 year old won’t poop on potty. 5. Take your child to the potty frequently\nFrustrated when your child has potty training accidents just minutes after he said he didn’t need to use the potty? Don’t wait until he asks to use the potty—take him frequently so he has a better chance of peeing in the potty instead of on the floor. You can even use a timer and set it to every 30 minutes to an hour for a potty break, so it feels more “official” than telling him what to do. But don’t feel disappointed if most of these tries end up with no pee in the potty—you wouldn’t be able to pee either if you were to go this often. The point is to increase the chances of peeing in the potty through frequent trips. And make potty use a regular part of his day. Routines give him the predictability he needs so he knows exactly what to do and when. You might use the potty after waking up, before leaving the house, after eating meals, or before bath time.", 
    "start_char": 8952, 
    "end_char": 9928
},
...
```

### Output from user
Output in TREC format containing top-k=`100` MSMARCOv2 segments as TSV: <`r_output_trec_rag_2024.tsv`>:

```bash
...
# Example of how to return the top-k qrels
2029747 Q0  msmarco_v2.1_doc_51_822664157#2 1
2029747 Q0  msmarco_v2.1_doc_51_822664157#1 1
2029747 Q0  msmarco_v2.1_doc_51_822664157#5 1
2029747 Q0  msmarco_v2.1_doc_51_822664157#6 1
2029747 Q0  msmarco_v2.1_doc_51_822664157#0 1
2029747 Q0  msmarco_v2.1_doc_28_505998624#22    1
...
```

## TASK 2: Augmented Generation Track (AG)

- **Given**: Participants will be provided a list of topics and top-k relevant retrieved segments mapped with the complete MSMARCO v2.1 segment collection.
- **Task**: Return the summarized answer ground based on the information available in the pre-determined list of top-k segments provided to the participant. 
- **Notes**: The AG track is for the NLP audience, focused on the generation output and quality. We provide the top-k retrieved segments, which allows the participants to focus on the RAG generation quality, by grounding on the set of chunks of segments, and generate an informative RAG summarized answer.

### Inputs to user
1. List of queries as topics as TSV: <`trec_rag_queries.tsv`>

```bash
# Example of `trec_rag_queries.tsv`
...
2027497	how often should you take your toddler to the potty when potty training
300986	how many years in jail for money laundering
835760	what is the name of the triangular region at the base of the bladder?
...
```

2. MSMARCOv2.1 segment corpus as JSONL: <`msmarco_v2.1_doc_segmented_XX.json.gz`>

```python
# Example of `msmarco_v2.1_doc_segmented_XX.json.gz`
...
{
    "docid": "msmarco_v2.1_doc_51_822664157#2", 
    "url": "https://www.romper.com/p/how-often-should-i-take-my-toddler-to-the-potty-there-are-some-guidelines-to-follow-71586", 
    "title": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "headings": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nHow Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "segment": "Self-esteem can be fragile at this time, so it's important to toilet train gently, letting your child lead the way. Additionally, it's unwise to begin potty training unless your child is truly ready. Take this potty training readiness quiz featured in Parents before you begin. Elizabeth Pantley, author of The No-Cry Potty Training Solution, explained in an excerpt on Child Development Info that most toddlers pee four to eight times per day. On top of that, toddlers have one or two bowel movements a day. But every toddler is an individual. Some will go more often than that, and others will last a couple days without having a bowel movement at all. In terms of actually getting your toddler to the potty, Pantley suggested setting up a potty routine. Potty first thing in the morning, after eating, and before other activities, like riding in the car or going to sleep. Of course, you can adapt this routine to your lifestyle, and you still must be on the lookout for signs your toddler has to go ahead of schedule.", 
    "start_char": 1445, 
    "end_char": 2466
},
{
    "docid": "msmarco_v2.1_doc_28_505998624#22", 
    "url": "https://sleepingshouldbeeasy.com/potty-training-accidents/", 
    "title": "Potty Trained Toddler Having Accidents on Purpose?", 
    "headings": "Secrets to Fixing Your Toddler’s Potty Training Accidents\nSecrets to Fixing Your Toddler’s Potty Training Accidents\nTable of Contents\nHow to handle a potty trained toddler having accidents on purpose\nWhy potty training accidents happen\n1. Stop the rewards\nLearn more about why rewards don’t always work.\n2. Don’t label your child in negative ways\nLearn more about the downsides of labeling our kids.\n3. Go back to the drawing board\nLearn what to do when your toddler won’t poop on the potty.\n4. Watch your reaction\nGet tips on what to do when your 4 year old won’t poop on potty.\n5. Take your child to the potty frequently\nGet more tips on how to ease your child’s potty training poop anxiety.\n6. Practice good potty training habits\nLearn why you shouldn’t worry when your toddler refuses to sit on potty.\nConclusion\n", 
    "segment": "Get tips on what to do when your 4 year old won’t poop on potty. 5. Take your child to the potty frequently\nFrustrated when your child has potty training accidents just minutes after he said he didn’t need to use the potty? Don’t wait until he asks to use the potty—take him frequently so he has a better chance of peeing in the potty instead of on the floor. You can even use a timer and set it to every 30 minutes to an hour for a potty break, so it feels more “official” than telling him what to do. But don’t feel disappointed if most of these tries end up with no pee in the potty—you wouldn’t be able to pee either if you were to go this often. The point is to increase the chances of peeing in the potty through frequent trips. And make potty use a regular part of his day. Routines give him the predictability he needs so he knows exactly what to do and when. You might use the potty after waking up, before leaving the house, after eating meals, or before bath time.", 
    "start_char": 8952, 
    "end_char": 9928
},
...
```

3. Oracle segments from the MSMARCOv2.1 corpus: <`trec_rag_qrels_oracle_segments.tsv`>
```bash
# Example of the input oracle segments `trec_rag_qrels_oracle_segments.tsv`
...
2029747 Q0  msmarco_v2.1_doc_51_822664157#2 1
2029747 Q0  msmarco_v2.1_doc_51_822664157#1 1
2029747 Q0  msmarco_v2.1_doc_51_822664157#5 1
2029747 Q0  msmarco_v2.1_doc_51_822664157#6 1
2029747 Q0  msmarco_v2.1_doc_51_822664157#0 1
2029747 Q0  msmarco_v2.1_doc_28_505998624#22    1
2029747 Q0  msmarco_v2.1_doc_10_1409639728#18   1
2029747 Q0  msmarco_v2.1_doc_08_978560686#8 1
2029747 Q0  msmarco_v2.1_doc_13_493603038#21    1
2029747 Q0  msmarco_v2.1_doc_08_978560686#7 1
2029747 Q0  msmarco_v2.1_doc_49_468284243#11    1
2029747 Q0  msmarco_v2.1_doc_08_978560686#13    1
2029747 Q0  msmarco_v2.1_doc_28_505998624#23    1
2029747 Q0  msmarco_v2.1_doc_28_505826468#17    1
2029747 Q0  msmarco_v2.1_doc_49_468284243#10    1
2029747 Q0  msmarco_v2.1_doc_13_493603038#20    1
2029747 Q0  msmarco_v2.1_doc_47_538801269#0 1
2029747 Q0  msmarco_v2.1_doc_29_1257953385#5    1
2029747 Q0  msmarco_v2.1_doc_08_978560686#12    1
2029747 Q0  msmarco_v2.1_doc_57_1426982301#15   1
...
```

### Output from user
Output containing the following JSON information as <`ag_output_trec_rag_2024.jsonl`>:

```python
{
    "topic_id": "2027497",  # query_id
    "topic": "how often should you take your toddler to the potty when potty training",  # query
    "references": [ # top-k segments returned used from the retrieval step. We have k equals to 20 segments.
        "msmarco_v2.1_doc_51_822664157#2", "msmarco_v2.1_doc_51_822664157#1", "msmarco_v2.1_doc_51_822664157#5", 
        "msmarco_v2.1_doc_51_822664157#6", "msmarco_v2.1_doc_51_822664157#0", "msmarco_v2.1_doc_28_505998624#22", 
        "msmarco_v2.1_doc_10_1409639728#18", "msmarco_v2.1_doc_08_978560686#8", "msmarco_v2.1_doc_13_493603038#21", 
        "msmarco_v2.1_doc_08_978560686#7", "msmarco_v2.1_doc_49_468284243#11", "msmarco_v2.1_doc_08_978560686#13", 
        "msmarco_v2.1_doc_28_505998624#23", "msmarco_v2.1_doc_28_505826468#17", "msmarco_v2.1_doc_49_468284243#10", 
        "msmarco_v2.1_doc_13_493603038#20", "msmarco_v2.1_doc_47_538801269#0", "msmarco_v2.1_doc_29_1257953385#5", 
        "msmarco_v2.1_doc_08_978560686#12", "msmarco_v2.1_doc_57_1426982301#15"
        ],
    "response_length": 586, # total length of the AG response
    "answer": [ # list of answer broken into sentences with each sentence having a citation containing index of document in references.
        {"text": "There is no magic number for how often you should take your toddler to the potty when potty training.", "citations": [2, 3]}, 
        {"text": "However, it is recommended to take them often, and to follow a schedule.", "citations": [2, 3, 5, 12]}, 
        {"text": "For example, you could take them first thing in the morning, before nap time, and before other activities such as riding in the car or going to sleep.", "citations": [0, 2, 3, 5, 7, 9, 12]}, 
        {"text": "You could also use a timer and set it to every 30 minutes to an hour for a potty break.", "citations": [5, 6, 8, 15]}, 
        {"text": "It is important to remember to look out for signs that your toddler needs to go ahead of schedule, and to keep your emotions in check throughout the potty-training process.", "citations": [0, 2, 3]}
    ]
}
```

## TASK 3: Retrieval-Augmented Generation Track (RAG)

- **Given**: Participants will be provided a list of topics and the complete MSMARCO v2 document/segment collection. 
- **Task**: Return the summarized answer and ground based on information which you can either the MSMARCOv2 document or segment collection. Develop your own retrieval system to fetch relevant information from the MSMARCOv2 segment/document collection. You can use either our pre-determined segment collection or incorporate your own **chunking** technique with the MSMARCOv2 document collection.
- **Notes**: The RAG track is a mixture of above (R) and (AG) tracks. This setup mimics best the industrial RAG setup for the NLP+IR audience. We evaluate the summarized answer in multiple ways incorporating both grounding and evaluating fluency of the generated output.

### Inputs to user

1. List of queries as topics as TSV: <`trec_rag_queries.tsv`>

```bash
# Example of `trec_rag_queries.tsv`
...
2027497	how often should you take your toddler to the potty when potty training
300986	how many years in jail for money laundering
835760	what is the name of the triangular region at the base of the bladder?
...
```

2. MSMARCOv2.1 segment/document corpus: <`msmarco_v2.1_doc_segmented_XX.json.gz`>

```python
# Example of `msmarco_v2.1_doc_segmented_XX.json.gz`
# `msmarco_v2.1_doc_00_X` denotes the document_id and `#X` denotes the segment_id identifier, e.g. `msmarco_v2.1_doc_00_4#2` is the 2nd segment in the document `msmarco_v2.1_doc_00_4`
...
{
    "docid": "msmarco_v2.1_doc_51_822664157#2", 
    "url": "https://www.romper.com/p/how-often-should-i-take-my-toddler-to-the-potty-there-are-some-guidelines-to-follow-71586", 
    "title": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "headings": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nHow Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "segment": "Self-esteem can be fragile at this time, so it's important to toilet train gently, letting your child lead the way. Additionally, it's unwise to begin potty training unless your child is truly ready. Take this potty training readiness quiz featured in Parents before you begin. Elizabeth Pantley, author of The No-Cry Potty Training Solution, explained in an excerpt on Child Development Info that most toddlers pee four to eight times per day. On top of that, toddlers have one or two bowel movements a day. But every toddler is an individual. Some will go more often than that, and others will last a couple days without having a bowel movement at all. In terms of actually getting your toddler to the potty, Pantley suggested setting up a potty routine. Potty first thing in the morning, after eating, and before other activities, like riding in the car or going to sleep. Of course, you can adapt this routine to your lifestyle, and you still must be on the lookout for signs your toddler has to go ahead of schedule.", 
    "start_char": 1445, 
    "end_char": 2466
},
{
    "docid": "msmarco_v2.1_doc_28_505998624#22", 
    "url": "https://sleepingshouldbeeasy.com/potty-training-accidents/", 
    "title": "Potty Trained Toddler Having Accidents on Purpose?", 
    "headings": "Secrets to Fixing Your Toddler’s Potty Training Accidents\nSecrets to Fixing Your Toddler’s Potty Training Accidents\nTable of Contents\nHow to handle a potty trained toddler having accidents on purpose\nWhy potty training accidents happen\n1. Stop the rewards\nLearn more about why rewards don’t always work.\n2. Don’t label your child in negative ways\nLearn more about the downsides of labeling our kids.\n3. Go back to the drawing board\nLearn what to do when your toddler won’t poop on the potty.\n4. Watch your reaction\nGet tips on what to do when your 4 year old won’t poop on potty.\n5. Take your child to the potty frequently\nGet more tips on how to ease your child’s potty training poop anxiety.\n6. Practice good potty training habits\nLearn why you shouldn’t worry when your toddler refuses to sit on potty.\nConclusion\n", 
    "segment": "Get tips on what to do when your 4 year old won’t poop on potty. 5. Take your child to the potty frequently\nFrustrated when your child has potty training accidents just minutes after he said he didn’t need to use the potty? Don’t wait until he asks to use the potty—take him frequently so he has a better chance of peeing in the potty instead of on the floor. You can even use a timer and set it to every 30 minutes to an hour for a potty break, so it feels more “official” than telling him what to do. But don’t feel disappointed if most of these tries end up with no pee in the potty—you wouldn’t be able to pee either if you were to go this often. The point is to increase the chances of peeing in the potty through frequent trips. And make potty use a regular part of his day. Routines give him the predictability he needs so he knows exactly what to do and when. You might use the potty after waking up, before leaving the house, after eating meals, or before bath time.", 
    "start_char": 8952, 
    "end_char": 9928
},
...
```


### Output from user
Output containing the following JSON information as <`rag_output_trec_rag_2024.jsonl`>. You can feel free to use any document/segmentation choice of yours, however, to make this collection reusable, we require the participant to map their custom chunked segments with segments available from MSMARCO v2.1 segment collection and provide us back the JSON output shown below:

```python
{
    "topic_id": "2027497",  # query_id
    "topic": "how often should you take your toddler to the potty when potty training",  # query
    "references": [ # top-k segments returned used from the retrieval step. We have k equals to 20 segments.
        "msmarco_v2.1_doc_51_822664157#2", "msmarco_v2.1_doc_51_822664157#1", "msmarco_v2.1_doc_51_822664157#5", 
        "msmarco_v2.1_doc_51_822664157#6", "msmarco_v2.1_doc_51_822664157#0", "msmarco_v2.1_doc_28_505998624#22", 
        "msmarco_v2.1_doc_10_1409639728#18", "msmarco_v2.1_doc_08_978560686#8", "msmarco_v2.1_doc_13_493603038#21", 
        "msmarco_v2.1_doc_08_978560686#7", "msmarco_v2.1_doc_49_468284243#11", "msmarco_v2.1_doc_08_978560686#13", 
        "msmarco_v2.1_doc_28_505998624#23", "msmarco_v2.1_doc_28_505826468#17", "msmarco_v2.1_doc_49_468284243#10", 
        "msmarco_v2.1_doc_13_493603038#20", "msmarco_v2.1_doc_47_538801269#0", "msmarco_v2.1_doc_29_1257953385#5", 
        "msmarco_v2.1_doc_08_978560686#12", "msmarco_v2.1_doc_57_1426982301#15"
        ],
    "response_length": 586, # total length of the RAG response
    "answer": [ # list of answer broken into sentences with each sentence having a citation containing index of document in references.
        {"text": "There is no magic number for how often you should take your toddler to the potty when potty training.", "citations": [2, 3]}, 
        {"text": "However, it is recommended to take them often, and to follow a schedule.", "citations": [2, 3, 5, 12]}, 
        {"text": "For example, you could take them first thing in the morning, before nap time, and before other activities such as riding in the car or going to sleep.", "citations": [0, 2, 3, 5, 7, 9, 12]}, 
        {"text": "You could also use a timer and set it to every 30 minutes to an hour for a potty break.", "citations": [5, 6, 8, 15]}, 
        {"text": "It is important to remember to look out for signs that your toddler needs to go ahead of schedule, and to keep your emotions in check throughout the potty-training process.", "citations": [0, 2, 3]}
    ]
}
```

We now pass this on to the community for feedback. Please feel free to reach out to us via email/Twitter/Discord!

Live Long and Prosper,
TREC RAG Organizers