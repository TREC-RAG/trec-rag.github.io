---
title: "TREC 2024 RAG Track Guidelines"
date: 2024-07-09T09:00:00-00:00
categories:
  - Annoucements
tags:
  - Guidelines
  - Evaluation
  - TREC 2024
  - Tasks
classes: wide
toc: false
---

# TREC 2024 RAG Guidelines

> Version 1.0. Last Updated: July 9, 2024

Participating teams will receive both the MS MARCO V2.1 document \& segment collection and a list of topic descriptions.
For each topic, participants have the choice to participate in either all or any of three tasks introduced this RAG this year. For the Retrieval Track (R), participating systems would provide a ranked list of segment IDs retrieved from the MS MARCO V2.1 segment collection. Next, for tracks with Augmented Generation (AG \& RAG), participating systems would generate an answer description (containing upto a maximum of 300 words) broken into individual sentences with citations from the MS MARCO V2.1 segment collection.

> Participate in our RAG Track by registering for TREC at this [website](https://trec.nist.gov/pubs/call2024.html).

> Test topics will be released by August 4, 2024 \& Submit your participating runs by August 11, 2024!

## Task Overview

We are excited to provide details on each task which will be conducted in the first year of the TREC RAG track! 🎉🎉

| TREC 2024 RAG Task  | Input | Output |
| ------------------- | ----- | ------ |
| [(R) Retrieval Task](#retrieval-task-r) | MS MARCO V2.1 Segment Collection + List of Topics | Ranked List of Segment IDs drawn from the collection |
| [(AG) Augmented Generation Task](#augmented-generation-task-ag) | Ranked List of Segment IDs + List of Topics | RAG Answer with references from provided Segment IDs |
| [(RAG) Retrieval-Augmented Generation Task](#retrieval-augmented-generation-task-rag) | MS MARCO V2.1 Segment \& Document Collection + List of Topics | RAG Answer with references from provided Segment IDs |


## Assessment \& Evaluation
Evaluation of the participating systems will involve four metrics: *Nugget evaluation*, *Support evaluation*, *Fluency evaluation* \& *Retrieval evaluation*. All cited segments provided by the partcipants will be added to the relevance assessment pools for each individual topic. After the first round of LLM-generated relevance assessments with post-curation from NIST assessors, the LLM-generated nugget list for nugget evaluation with post-curation from NIST assessors. Finally, we assign scores based on nugget recall and precision and other factors involving LLM-assisted support evaluation (grouding based on referenced segments) and LLM-assisted fluency evaluation (grammar and coherence) of the RAG response with post-curation from NIST assessors. The detailed process for assessment will be outlined soon.


# Task Overview

## Retrieval Task (R)
The retrieval task as the name suggets is an ad-hoc information retrieval task similar to the previous [TREC Deep Learning Track](https://microsoft.github.io/msmarco/TREC-Deep-Learning.html). Participating systems will receive a list of topics and the MS MARCO V2.1 segment collection. For each topic, the system needs to return the TREC runfile containing the ranked list containing the top 20 relevant segment IDs from the collection. The topics provided will be non-factoid and require long-form answer generation.

> The “R” track emulates the previous TREC-DL 2022/2023 tracks is for the IR audience, however, the main difference lies in using document *chunks* from the MS MARCO V2.1 segment collection instead of the MS MARCO v2.0 passage collection.

### Input Format (Topics)

List of queries as topics as TSV: <`trec_rag_2024_queries.tsv`>, with each line containing the topic_id and a sentence-length description of the topic.

```bash
# Example of `trec_rag_2024_queries.tsv`
...
2027497	how often should you take your toddler to the potty when potty training
300986	how many years in jail for money laundering
835760	what is the name of the triangular region at the base of the bladder?
...
```

### Input Format (Segments)

MS MARCO v2.1 segment collection as JSONL: <`msmarco_v2.1_doc_segmented_XX.json.gz`>, each document is present in the JSON format on each line. The fields present for each document are:
- docid (string): The segment ID for the MS MARCO v2.1 segment (Note: ID before "#" is the mapped document ID)
- url (string): The url of the segment available on the webpage (same as the document)
- title (string): The title of the segment or chunk (same as the document) 
- headings (string): The headings available in the segment or chunk (same as the document)
- segment (string): The complete text of the segment or chunk
- start_char (integer): The start character of the segment or chunk in the mapped document
- end_char (integer): The end character of the segment or chunk in the mapped document


```python
# Example of `msmarco_v2.1_doc_segmented_XX.json.gz`
...
{
    "docid": "msmarco_v2.1_doc_51_766815931#2_1606878413", 
    "url": "https://www.romper.com/p/how-often-should-i-take-my-toddler-to-the-potty-there-are-some-guidelines-to-follow-71586", 
    "title": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "headings": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nHow Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "segment": "Self-esteem can be fragile at this time, so it's important to toilet train gently, letting your child lead the way. Additionally, it's unwise to begin potty training unless your child is truly ready. Take this potty training readiness quiz featured in Parents before you begin. Elizabeth Pantley, author of The No-Cry Potty Training Solution, explained in an excerpt on Child Development Info that most toddlers pee four to eight times per day. On top of that, toddlers have one or two bowel movements a day. But every toddler is an individual. Some will go more often than that, and others will last a couple days without having a bowel movement at all. In terms of actually getting your toddler to the potty, Pantley suggested setting up a potty routine. Potty first thing in the morning, after eating, and before other activities, like riding in the car or going to sleep. Of course, you can adapt this routine to your lifestyle, and you still must be on the lookout for signs your toddler has to go ahead of schedule.", 
    "start_char": 1445, 
    "end_char": 2466
},
{
    "docid": "msmarco_v2.1_doc_37_463237391#10_984448281", 
    "url": "https://www.curejoy.com/content/how-to-potty-train-your-kid/",
    "title": "How To Potty Train Your Kid: Toilet Training Tips For Toddlers | CureJoy", 
    "headings": "How To Potty Train Your Kid: Toilet Training Tips For Toddlers\nHow To Potty Train Your Kid: Toilet Training Tips For Toddlers\n1. Start Potty Training At “The Right Time”\n2. Watch For Cues From Your Child\n3. Understand Your Child’s Temperament\n4. Create a Potty Training Plan\nRead To Your Child\nBuy A Good Potty Chair Or Seat\nLet Your Toddler Become Comfortable\nCreate A Schedule\nPraise, Praise, Praise\nPatience Is A Virtue!\n5. Stick To These Potty Training Dos\n6. And Steer Clear Of These Don’ts!\n", 
    "segment": "Take your child to the potty about 3 times a day – first thing in the morning, after mealtimes, and again before bedtime. It should become part of their daily routine. About 30 minutes after a meal is a good time to try. Also watch for facial expressions or poses that may signal that they need to “go.” If you take your toddler to the potty and they are reluctant to use it, don’t force them. But if they agree to get\nAdvertisements\non it, lavish praise on them and give a small reward even if they don’t actually poop or pee. Over time, your child will get the hang of what they’re supposed to do. It takes about 3–6 months to reliably potty train your toddler, so patience is key. Most kids still wear diapers overnight until age 5, because nighttime control is more difficult to attain. 6\nPraise, Praise, Praise\nThis is the most crucial part of the plan!", 
    "start_char": 4551, 
    "end_char": 5409
},
...
```

### Output Format (Ranked Results)
Participants should provide their output in the standard TREC format containing top-k=`20` MS MARCO v2.1 segments as TSV: <`r_output_trec_rag_2024.tsv`> for each individual topic. Each set of ranked results for a set of topics appears in a single file. We will take a maximum of 20 results from each participant, more than 20 results will be truncated. Each line of this file contains six whitespace-separated entries:
- Topic ID (taken from `trec_rag_2024_queries.tsv`)
- The fixed string “Q0”
- Segment ID (from the docid field in `msmarco_v2.1_doc_segmented_XX.json.gz`)
- Score (integer or float, selected by your system)
- Run ID where you should mention your team-name (e.g. my-team-name)


```bash
...
# Example of how to return the top-k qrels
2027497 Q0 msmarco_v2.1_doc_51_766815931#2_1606878413 0.99986017 my-team-name
2027497 Q0 msmarco_v2.1_doc_51_766815931#1_1606876582 0.9996673 my-team-name
2027497 Q0 msmarco_v2.1_doc_51_766815931#5_1606882767 0.99931216 my-team-name
2027497 Q0 msmarco_v2.1_doc_51_766815931#6_1606884302 0.99923867 my-team-name
2027497 Q0 msmarco_v2.1_doc_51_766815931#3_1606879951 0.99862224 my-team-name
2027497 Q0 msmarco_v2.1_doc_51_766815931#4_1606881348 0.9985786 my-team-name
2027497 Q0 msmarco_v2.1_doc_37_463237391#10_984448281 0.99851626 my-team-name
2027497 Q0 msmarco_v2.1_doc_51_766815931#0_1606874600 0.9980733 my-team-name
2027497 Q0 msmarco_v2.1_doc_37_463237391#9_984446615 0.99794924 my-team-name
2027497 Q0 msmarco_v2.1_doc_28_472446307#22_1012988885 0.99647564 my-team-name
2027497 Q0 msmarco_v2.1_doc_51_766815931#7_1606885873 0.9926826 my-team-name
2027497 Q0 msmarco_v2.1_doc_28_472446307#21_1012986800 0.9922143 my-team-name
2027497 Q0 msmarco_v2.1_doc_29_562342450#23_1356565296 0.9852146 my-team-name
2027497 Q0 msmarco_v2.1_doc_29_562342450#17_1356555947 0.9829547 my-team-name
2027497 Q0 msmarco_v2.1_doc_49_418787959#7_861728734 0.97997653 my-team-name
2027497 Q0 msmarco_v2.1_doc_49_418787959#6_861726964 0.9739437 my-team-name
2027497 Q0 msmarco_v2.1_doc_26_680625866#7_1289507527 0.97334224 my-team-name
2027497 Q0 msmarco_v2.1_doc_10_1346272776#19_2165266355 0.9732915 my-team-name
2027497 Q0 msmarco_v2.1_doc_56_1491300640#3_3012150696 0.97272736 my-team-name
2027497 Q0 msmarco_v2.1_doc_10_672519892#5_1260010758 0.9719925 my-team-name
...
```

## Augmented Generation Task (AG)

The Augmented Generation task emulates the modern-day RAG task to return the summarized answer ground based on the information available in the pre-determined list of top-k segments provided to the participant.  Participating systems will receive a list of topics, MS MARCO V2.1 segment collection and the ranked list of the top-k relevant segments for each individual topic. The topics provided will be non-factoid and require long-form answer generation.

> The AG track is for the NLP audience, focused on the generation output and quality. We provide the top-k retrieved segments, which allows the participants to focus on the RAG generation quality, by grounding on the set of chunks of segments, and generate an informative RAG summarized answer.

### Input Format (Topics)

List of queries as topics as TSV: <`trec_rag_2024_queries.tsv`>, with each line containing the topic_id and a sentence-length description of the topic.

```bash
# Example of `trec_rag_2024_queries.tsv`
...
2027497	how often should you take your toddler to the potty when potty training
300986	how many years in jail for money laundering
835760	what is the name of the triangular region at the base of the bladder?
...
```

### Input Format (Segments)

MS MARCO v2.1 segment collection as JSONL: <`msmarco_v2.1_doc_segmented_XX.json.gz`>, each document is present in the JSON format on each line. The fields present for each document are:
- docid (string): The segment ID for the MS MARCO v2.1 segment (Note: ID before "#" is the mapped document ID)
- url (string): The url of the segment available on the webpage (same as the document)
- title (string): The title of the segment or chunk (same as the document) 
- headings (string): The headings available in the segment or chunk (same as the document)
- segment (string): The complete text of the segment or chunk
- start_char (integer): The start character of the segment or chunk in the mapped document
- end_char (integer): The end character of the segment or chunk in the mapped document


```python
# Example of `msmarco_v2.1_doc_segmented_XX.json.gz`
...
{
    "docid": "msmarco_v2.1_doc_51_766815931#2_1606878413", 
    "url": "https://www.romper.com/p/how-often-should-i-take-my-toddler-to-the-potty-there-are-some-guidelines-to-follow-71586", 
    "title": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "headings": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nHow Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "segment": "Self-esteem can be fragile at this time, so it's important to toilet train gently, letting your child lead the way. Additionally, it's unwise to begin potty training unless your child is truly ready. Take this potty training readiness quiz featured in Parents before you begin. Elizabeth Pantley, author of The No-Cry Potty Training Solution, explained in an excerpt on Child Development Info that most toddlers pee four to eight times per day. On top of that, toddlers have one or two bowel movements a day. But every toddler is an individual. Some will go more often than that, and others will last a couple days without having a bowel movement at all. In terms of actually getting your toddler to the potty, Pantley suggested setting up a potty routine. Potty first thing in the morning, after eating, and before other activities, like riding in the car or going to sleep. Of course, you can adapt this routine to your lifestyle, and you still must be on the lookout for signs your toddler has to go ahead of schedule.", 
    "start_char": 1445, 
    "end_char": 2466
},
{
    "docid": "msmarco_v2.1_doc_37_463237391#10_984448281", 
    "url": "https://www.curejoy.com/content/how-to-potty-train-your-kid/",
    "title": "How To Potty Train Your Kid: Toilet Training Tips For Toddlers | CureJoy", 
    "headings": "How To Potty Train Your Kid: Toilet Training Tips For Toddlers\nHow To Potty Train Your Kid: Toilet Training Tips For Toddlers\n1. Start Potty Training At “The Right Time”\n2. Watch For Cues From Your Child\n3. Understand Your Child’s Temperament\n4. Create a Potty Training Plan\nRead To Your Child\nBuy A Good Potty Chair Or Seat\nLet Your Toddler Become Comfortable\nCreate A Schedule\nPraise, Praise, Praise\nPatience Is A Virtue!\n5. Stick To These Potty Training Dos\n6. And Steer Clear Of These Don’ts!\n", 
    "segment": "Take your child to the potty about 3 times a day – first thing in the morning, after mealtimes, and again before bedtime. It should become part of their daily routine. About 30 minutes after a meal is a good time to try. Also watch for facial expressions or poses that may signal that they need to “go.” If you take your toddler to the potty and they are reluctant to use it, don’t force them. But if they agree to get\nAdvertisements\non it, lavish praise on them and give a small reward even if they don’t actually poop or pee. Over time, your child will get the hang of what they’re supposed to do. It takes about 3–6 months to reliably potty train your toddler, so patience is key. Most kids still wear diapers overnight until age 5, because nighttime control is more difficult to attain. 6\nPraise, Praise, Praise\nThis is the most crucial part of the plan!", 
    "start_char": 4551, 
    "end_char": 5409
},
...
```

### Input Format (Ranked Results)

Top-20 retrieved segments using our baseline retrieval system on the MS MARCO v2.1 segment collection: <`trec_rag_2024_qrels.tsv`> for each individual topic. Each set of ranked results for a set of topics appears in a single file. We will provide a maximum of 20 segments for each individual topic. Each line of this file contains four whitespace-separated entries:
- Topic ID (taken from `trec_rag_2024_queries.tsv`)
- The fixed string “Q0”
- Segment ID (from the docid field in `msmarco_v2.1_doc_segmented_XX.json.gz`)
- Score of 1 (indicating the segment contains relevant information for the topic)

```bash
# Example of the input oracle segments `trec_rag_2024_qrels.tsv`
...
2027497 Q0  msmarco_v2.1_doc_51_766815931#2_1606878413  1
2027497 Q0  msmarco_v2.1_doc_51_766815931#1_1606876582  1
2027497 Q0  msmarco_v2.1_doc_51_766815931#5_1606882767  1
2027497 Q0  msmarco_v2.1_doc_51_766815931#6_1606884302  1
2027497 Q0  msmarco_v2.1_doc_51_766815931#3_1606879951  1
2027497 Q0  msmarco_v2.1_doc_51_766815931#4_1606881348  1
2027497 Q0  msmarco_v2.1_doc_37_463237391#10_984448281  1
2027497 Q0  msmarco_v2.1_doc_51_766815931#0_1606874600  1
2027497 Q0  msmarco_v2.1_doc_37_463237391#9_984446615   1
2027497 Q0  msmarco_v2.1_doc_28_472446307#22_1012988885 1
2027497 Q0  msmarco_v2.1_doc_51_766815931#7_1606885873  1
2027497 Q0  msmarco_v2.1_doc_28_472446307#21_1012986800 1
2027497 Q0  msmarco_v2.1_doc_29_562342450#23_1356565296 1
2027497 Q0  msmarco_v2.1_doc_29_562342450#17_1356555947 1
2027497 Q0  msmarco_v2.1_doc_49_418787959#7_861728734   1
2027497 Q0  msmarco_v2.1_doc_49_418787959#6_861726964   1
2027497 Q0  msmarco_v2.1_doc_26_680625866#7_1289507527  1
2027497 Q0  msmarco_v2.1_doc_10_1346272776#19_2165266355    1
2027497 Q0  msmarco_v2.1_doc_56_1491300640#3_3012150696 1
2027497 Q0  msmarco_v2.1_doc_10_672519892#5_1260010758  1
...
```

### Output Format (AG Output)

Participants should provide their output in the standard JSONL format containing the following JSON information as <`ag_output_trec_rag_2024.jsonl`> for each individual topic. The final RAG answer should provided in the following JSON format. Each line of this JSONL file contains the following entries:

- run_id (string) containing your team name (e.g. "my-awesome-team-name")
- topic_id (string) from the topic_id taken from `trec_rag_2024_queries.tsv`
- topic (string) the sentence-level description of the topic taken from `trec_rag_2024_queries.tsv`
- references (array) containing the ranked list of top-k segment IDs from the retrieval stage (a maximum of only 20 segments is allowed)
- response_length (integer) containing the total words present in the overall RAG response.
- answer (array) containing the list of sentences and citations from the `references` list. The `text` field contains the response and `citations` field contains the (zero-indexed) reference of the segment from the `references` list.

```python
{
    "run_id": "my-awesome-team-name",
    "topic_id": "2027497", # query_id
    "topic": "how often should you take your toddler to the potty when potty training", # query
    "references": [ # top-k segments returned used from the retrieval step. We have k equals to 20 segments for this example.
        "msmarco_v2.1_doc_51_766815931#2_1606878413", "msmarco_v2.1_doc_51_766815931#1_1606876582", "msmarco_v2.1_doc_51_766815931#5_1606882767", 
        "msmarco_v2.1_doc_51_766815931#6_1606884302", "msmarco_v2.1_doc_51_766815931#3_1606879951", "msmarco_v2.1_doc_51_766815931#4_1606881348", 
        "msmarco_v2.1_doc_37_463237391#10_984448281", "msmarco_v2.1_doc_51_766815931#0_1606874600", "msmarco_v2.1_doc_37_463237391#9_984446615", 
        "msmarco_v2.1_doc_28_472446307#22_1012988885", "msmarco_v2.1_doc_51_766815931#7_1606885873", "msmarco_v2.1_doc_28_472446307#21_1012986800", 
        "msmarco_v2.1_doc_29_562342450#23_1356565296", "msmarco_v2.1_doc_29_562342450#17_1356555947", "msmarco_v2.1_doc_49_418787959#7_861728734", 
        "msmarco_v2.1_doc_49_418787959#6_861726964", "msmarco_v2.1_doc_26_680625866#7_1289507527", "msmarco_v2.1_doc_10_1346272776#19_2165266355", 
        "msmarco_v2.1_doc_56_1491300640#3_3012150696", "msmarco_v2.1_doc_10_672519892#5_1260010758"], 
    "response_length": 192, 
    "answer": [ # RAG answer broken into sentences with each answer sentence grounding information from the index mentioned in references.
            {"text": "The frequency with which you should take your toddler to the potty depends on their readiness for potty training.", "citations": [0, 1, 12, 13, 19]}, 
            {"text": "Some sources suggest that toddlers should be taken to the potty about three times a day: first thing in the morning, after mealtimes, and again before bedtime.", "citations": [0, 4, 6, 8]}, 
            {"text": "It is recommended that you watch for facial expressions or poses that may signal that they need to \"go\".", "citations": [6, 8]}, 
            {"text": "If they are reluctant to use the potty, don't force them.", "citations": [6, 8]}, 
            {"text": "Other sources suggest that toddlers should be taken to the potty every two hours, whether they have to go or not.", "citations": [14, 15]}, 
            {"text": "This includes first thing in the morning, before leaving the house, and before naps and bedtime.", "citations": [14, 15]}, 
            {"text": "Some sources recommend taking toddlers to the potty every 30 minutes to an hour.", "citations": [9, 11, 17]}, 
            {"text": "This is to increase the chances of them peeing in the potty instead of on the floor.", "citations": [9, 11]}, 
            {"text": "It is important to keep in mind that every toddler is different, and their potty training journey will be unique to them.", "citations": [0, 4]}, 
            {"text": "It is recommended that you let your toddler lead the way and be gentle throughout the process, as their self-esteem can be fragile during this time.", "citations": [0, 1]}
        ]
}
```

## Retrieval-Augmented Generation Task (RAG)

- **Given**: Participants will be provided a list of topics and both the MS MARCO v2.1 document and MS MARCO v2.1 segment collections. 
- **Task**: Return the summarized answer and ground based on information which you can either the MS MARCO v2.1 document or segment collection. Develop your own retrieval system to fetch relevant information from the MS MARCO v2.1 segment/document collection. You can use either our pre-determined segment collection or incorporate your own **chunking** technique with the MS MARCO v2.1 document collection. For evaluation, we ask each participant to map their chunk of segments with MS MARCO v2.1 segment collections.
- **Notes**: The RAG track is a mixture of above (R) and (AG) tracks. This setup mimics best the industrial RAG setup for the NLP+IR audience. We evaluate the summarized answer in multiple ways incorporating both grounding and evaluating fluency of the generated output.

### Input Format (Topics)

List of queries as topics as TSV: <`trec_rag_2024_queries.tsv`>, with each line containing the topic_id and a sentence-length description of the topic.

```bash
# Example of `trec_rag_2024_queries.tsv`
...
2027497	how often should you take your toddler to the potty when potty training
300986	how many years in jail for money laundering
835760	what is the name of the triangular region at the base of the bladder?
...
```

### Input Format (Documents)

MS MARCO v2.1 document collection as JSONL: <`msmarco_v2.1_doc_XX.json.gz`>, each document is present in the JSON format on each line. The fields present for each document are:
- docid (string): The document ID for the MS MARCO v2.1 document
- url (string): The url of the document
- title (string): The title of the document
- headings (string): The headings available in the document
- body (string): The complete text of the document

```python
# Example of `msmarco_v2.1_doc_XX.json.gz`
{
    'docid': 'msmarco_v2.1_doc_51_766815931',
    'url': 'https://www.romper.com/p/how-often-should-i-take-my-toddler-to-the-potty-there-are-some-guidelines-to-follow-71586', 
    'title': 'How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow', 
    'headings': 'How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nHow Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow', 
    'body': 'How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nLife\nAshley Batz/Romper\nHow Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nby Kelly Mullen-McWilliams\nJuly 22, 2017\nI don\'t know about you, but I\'m personally super pumped for that perfect day in the admittedly far-off future when I throw that last diaper away — and then throw myself a party. If you\'re currently in the midst of toilet training, I salute you, and I also know you have a lot of questions. Whether it\'s going well or not, you\'re probably wondering things like, " how often should I take my toddler to the potty ?"\nMore Like This\nVaccinated People Can Ditch Masks. Where Does That Leave Kids?\n25 Real-Life Reasons Not To Trust Older Siblings Around The Baby\nMoms To Toddlers Everywhere: This Aggression Will Not Stand, Man\nHow 20 Kids Brought The Pandemic Into Their Play Worlds\nWhat Parents Are Talking About — Delivered Straight To Your Inbox\nSubscribe\nAccording to an article in Pediatrics, the official journal of the American Academy of Pediatrics (AAP), independent toilet use is a major milestone for your child, combining new physical capabilities with an understanding of social expectations, and their own motivation to become more autonomous. The article noted that toilet training is also one of the most difficult milestones for children and their parents, and that it can become highly emotional. Self-esteem can be fragile at this time, so it\'s important to toilet train gently, letting your child lead the way. Additionally, it\'s unwise to begin potty training unless your child is truly ready. Take this potty training readiness quiz featured in Parents before you begin.\nElizabeth Pantley, author of The No-Cry Potty Training Solution, explained in an excerpt on Child Development Info that most toddlers pee four to eight times per day. On top of that, toddlers have one or two bowel movements a day. But every toddler is an individual. Some will go more often than that, and others will last a couple days without having a bowel movement at all.\nIn terms of actually getting your toddler to the potty, Pantley suggested setting up a potty routine. Potty first thing in the morning, after eating, and before other activities, like riding in the car or going to sleep. Of course, you can adapt this routine to your lifestyle, and you still must be on the lookout for signs your toddler has to go ahead of schedule. If he or she looks squirmy, take them to the potty. But if you miss the signal, and there\'s a mess, it\'s no big deal. Practice makes perfect, after all. Don\'t let emotions get the better of you, even if your little girl or guy pees on an expensive piece of furniture.\nTry to get your toddler to the toilet frequently, but remember that it\'s OK if she needs a day off. According to Becoming the Parent You Want To Be by Laura Davis and Janis Keyser, it\'s common for children to go back and forth — somedays preferring diapers, and other days selecting to use the toilet. They recommended thinking of "accidents" as "opportunities."\nPantley also suggested visiting new restrooms when you\'re on the go. Frequent visits to toilets far and near may help habituate your child to independent toilet use. Keep in mind that not all children will want to use strange bathrooms, and don\'t force anything. Davis and Keyser stressed the importance of keeping your own emotions in check throughout the toilet training process.\nThe bottom line: when it comes to potty time, there\'s no magic number, but it\'s a good idea to take your toddler to the toilet often. Begin by following a schedule — morning pee, before nap time pee — and remember to look for signs that they\'re holding it. You can only take your child to the bathroom too much if it begins to feel stressful or punitive. If negative emotions attach themselves to toilet time, it\'s OK to take a break. It might take some time to achieve that no-more-diapers party, but that\'s fine. You\'ll just have that much longer to plan a good one.\nMay 27. 2021\nSEARCH CLOSE\nPregnancy\nSee All Trying Birth After\nRaising Kids\nSee All Baby Toddler Little Kid Big Kid\nYou\nSee All Sex & Relationships Wellness Style\nLife\nSee All Food Home Entertainment Politics Shopping\nHealth\nAbout Archive Terms Privacy Newsletter Archive Advertise Masthead Editorial Standards\n© 2021 Bustle Digital Group. All rights reserved.'
}
```

### Input Format (Segments)

MS MARCO v2.1 segment collection as JSONL: <`msmarco_v2.1_doc_segmented_XX.json.gz`>, each document is present in the JSON format on each line. The fields present for each document are:
- docid (string): The segment ID for the MS MARCO v2.1 segment (Note: ID before "#" is the mapped document ID)
- url (string): The url of the segment available on the webpage (same as the document)
- title (string): The title of the segment or chunk (same as the document) 
- headings (string): The headings available in the segment or chunk (same as the document)
- segment (string): The complete text of the segment or chunk
- start_char (integer): The start character of the segment or chunk in the mapped document
- end_char (integer): The end character of the segment or chunk in the mapped document

```python
# Example of `msmarco_v2.1_doc_segmented_XX.json.gz`
...
{
    "docid": "msmarco_v2.1_doc_51_766815931#2_1606878413", 
    "url": "https://www.romper.com/p/how-often-should-i-take-my-toddler-to-the-potty-there-are-some-guidelines-to-follow-71586", 
    "title": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "headings": "How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nHow Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow", 
    "segment": "Self-esteem can be fragile at this time, so it's important to toilet train gently, letting your child lead the way. Additionally, it's unwise to begin potty training unless your child is truly ready. Take this potty training readiness quiz featured in Parents before you begin. Elizabeth Pantley, author of The No-Cry Potty Training Solution, explained in an excerpt on Child Development Info that most toddlers pee four to eight times per day. On top of that, toddlers have one or two bowel movements a day. But every toddler is an individual. Some will go more often than that, and others will last a couple days without having a bowel movement at all. In terms of actually getting your toddler to the potty, Pantley suggested setting up a potty routine. Potty first thing in the morning, after eating, and before other activities, like riding in the car or going to sleep. Of course, you can adapt this routine to your lifestyle, and you still must be on the lookout for signs your toddler has to go ahead of schedule.", 
    "start_char": 1445, 
    "end_char": 2466
},
{
    "docid": "msmarco_v2.1_doc_37_463237391#10_984448281", 
    "url": "https://www.curejoy.com/content/how-to-potty-train-your-kid/",
    "title": "How To Potty Train Your Kid: Toilet Training Tips For Toddlers | CureJoy", 
    "headings": "How To Potty Train Your Kid: Toilet Training Tips For Toddlers\nHow To Potty Train Your Kid: Toilet Training Tips For Toddlers\n1. Start Potty Training At “The Right Time”\n2. Watch For Cues From Your Child\n3. Understand Your Child’s Temperament\n4. Create a Potty Training Plan\nRead To Your Child\nBuy A Good Potty Chair Or Seat\nLet Your Toddler Become Comfortable\nCreate A Schedule\nPraise, Praise, Praise\nPatience Is A Virtue!\n5. Stick To These Potty Training Dos\n6. And Steer Clear Of These Don’ts!\n", 
    "segment": "Take your child to the potty about 3 times a day – first thing in the morning, after mealtimes, and again before bedtime. It should become part of their daily routine. About 30 minutes after a meal is a good time to try. Also watch for facial expressions or poses that may signal that they need to “go.” If you take your toddler to the potty and they are reluctant to use it, don’t force them. But if they agree to get\nAdvertisements\non it, lavish praise on them and give a small reward even if they don’t actually poop or pee. Over time, your child will get the hang of what they’re supposed to do. It takes about 3–6 months to reliably potty train your toddler, so patience is key. Most kids still wear diapers overnight until age 5, because nighttime control is more difficult to attain. 6\nPraise, Praise, Praise\nThis is the most crucial part of the plan!", 
    "start_char": 4551, 
    "end_char": 5409
},
...
```

### Output Format (RAG Output)
Output containing the following JSON information as <`rag_output_trec_rag_2024.jsonl`>. You can feel free to use the document collection with your own segmentation choice of yours, however, to make this collection reusable, we require the participant to map their custom chunked segments with segments available from MS MARCO V2.1 segment collection. Each line of this JSONL file contains the following entries:

- run_id (string) containing your team name (e.g. "my-awesome-team-name")
- topic_id (string) from the topic_id taken from `trec_rag_2024_queries.tsv`
- topic (string) the sentence-level description of the topic taken from `trec_rag_2024_queries.tsv`
- references (array) containing the ranked list of top-k segment IDs from the retrieval stage (a maximum of only 20 segments is allowed)
- response_length (integer) containing the total words present in the overall RAG response.
- answer (array) containing the list of sentences and citations from the `references` list. The `text` field contains the response and `citations` field contains the (zero-indexed) reference of the segment from the `references` list.

```python
{
    "run_id": "my-awesome-team-name",
    "topic_id": "2027497", # query_id
    "topic": "how often should you take your toddler to the potty when potty training", # query
    "references": [ # top-k segments returned used from the retrieval step. We have k equals to 20 segments for this example.
        "msmarco_v2.1_doc_51_766815931#2_1606878413", "msmarco_v2.1_doc_51_766815931#1_1606876582", "msmarco_v2.1_doc_51_766815931#5_1606882767", 
        "msmarco_v2.1_doc_51_766815931#6_1606884302", "msmarco_v2.1_doc_51_766815931#3_1606879951", "msmarco_v2.1_doc_51_766815931#4_1606881348", 
        "msmarco_v2.1_doc_37_463237391#10_984448281", "msmarco_v2.1_doc_51_766815931#0_1606874600", "msmarco_v2.1_doc_37_463237391#9_984446615", 
        "msmarco_v2.1_doc_28_472446307#22_1012988885", "msmarco_v2.1_doc_51_766815931#7_1606885873", "msmarco_v2.1_doc_28_472446307#21_1012986800", 
        "msmarco_v2.1_doc_29_562342450#23_1356565296", "msmarco_v2.1_doc_29_562342450#17_1356555947", "msmarco_v2.1_doc_49_418787959#7_861728734", 
        "msmarco_v2.1_doc_49_418787959#6_861726964", "msmarco_v2.1_doc_26_680625866#7_1289507527", "msmarco_v2.1_doc_10_1346272776#19_2165266355", 
        "msmarco_v2.1_doc_56_1491300640#3_3012150696", "msmarco_v2.1_doc_10_672519892#5_1260010758"], 
    "response_length": 192, 
    "answer": [ # RAG answer broken into sentences with each answer sentence grounding information from the index mentioned in references.
            {"text": "The frequency with which you should take your toddler to the potty depends on their readiness for potty training.", "citations": [0, 1, 12, 13, 19]}, 
            {"text": "Some sources suggest that toddlers should be taken to the potty about three times a day: first thing in the morning, after mealtimes, and again before bedtime.", "citations": [0, 4, 6, 8]}, 
            {"text": "It is recommended that you watch for facial expressions or poses that may signal that they need to \"go\".", "citations": [6, 8]}, 
            {"text": "If they are reluctant to use the potty, don't force them.", "citations": [6, 8]}, 
            {"text": "Other sources suggest that toddlers should be taken to the potty every two hours, whether they have to go or not.", "citations": [14, 15]}, 
            {"text": "This includes first thing in the morning, before leaving the house, and before naps and bedtime.", "citations": [14, 15]}, 
            {"text": "Some sources recommend taking toddlers to the potty every 30 minutes to an hour.", "citations": [9, 11, 17]}, 
            {"text": "This is to increase the chances of them peeing in the potty instead of on the floor.", "citations": [9, 11]}, 
            {"text": "It is important to keep in mind that every toddler is different, and their potty training journey will be unique to them.", "citations": [0, 4]}, 
            {"text": "It is recommended that you let your toddler lead the way and be gentle throughout the process, as their self-esteem can be fragile during this time.", "citations": [0, 1]}
        ]
}
```

## Next Steps

We encourage participants to start encoding the MS MARCO V2.1 segment corpus (120+ million) using their favourite retrieval system.
We will soon release the test topics and once released would give a single week submitting their participating runs.

We encourage the community to provide us with constructive feedback regarding any task, or require us to further clarify any task.
Please feel free to reach out to us via Twitter/Discord!

*The TREC RAG Organizers Send Their Regards.*