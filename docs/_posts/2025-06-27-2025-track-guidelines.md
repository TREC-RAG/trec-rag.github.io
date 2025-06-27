---
title: "TREC 2025 RAG Track Guidelines"
date: 2025-06-27T00:00:00-00:00
categories:
  - Annoucements
tags:
  - Guidelines
  - TREC 2025
  - Tasks
classes: wide
toc: false
---

Participating teams will receive both the MS MARCO V2.1 document & segment collection and a list of topic descriptions.
For each topic, participants have the choice to participate in either all or any of three tasks following last year's format. For the Retrieval Track (R), participating systems would provide a ranked list of segment IDs retrieved from the MS MARCO V2.1 segment collection. Next, for tracks with Augmented Generation (AG & RAG), participating systems would generate an answer description broken into individual sentences with citations from the MS MARCO V2.1 segment collection.

> Participate in our RAG Track by registering for TREC at this [website](https://trec.nist.gov).



# Tasks Overview

## Retrieval Task (R)
The retrieval task as the name suggets is an ad-hoc information retrieval task similar to the previous [TREC Deep Learning Track](https://microsoft.github.io/msmarco/TREC-Deep-Learning.html). Participating systems will receive a list of topics and the MS MARCO V2.1 segment collection. For each topic, the system needs to return the TREC runfile containing the ranked list containing the top 100 relevant segment IDs from the collection. The topics provided will be non-factoid 2-3 sentence long description and require long-form answer generation.

> The “R” track emulates the previous year's TREC R task and TREC-DL 2022/2023 tracks is for the IR audience, however, the main difference lies in using document *chunks* from the MS MARCO V2.1 segment collection instead of the MS MARCO v2.0 passage collection.

### Input Format (Topics)

List of queries as topics as JSONL: <`trec_rag_2025_queries.jsonl`>, with each line containing the id and a topic of 2-3 sentences long narrative description.

```bash
# Example of `trec_rag_2025_queries.jsonl`
...
[
    {
        "id": "1",
        "narrative": "I'm trying to understand how the Industrial Revolution began, what caused it, and how it changed societies, economies, and populations in different countries. I'm also interested in the roles of key figures like Henry Ford, the impact of technological advancements, and how industrialization connects to topics like urbanization, migration, and modern innovations such as robotics and extended reality."
    },
    {
        "id": "2",
        "narrative": "I'm trying to understand how prisons operate, including issues like inmate rights, rehabilitation, voting, and the impact of race and profit motives on incarceration. Can you explain how correctional facilities address mental health, discipline, and recidivism, and also discuss the ethical and legal challenges inmates face?"
    }
]
...
```

### Input Format (Segments)

MS MARCO v2.1 segment collection as JSONL: <`msmarco_v2.1_doc_segmented_XX.json.gz`>, each segment is present in the JSON format on each line. The fields present are:
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
    'docid': 'msmarco_v2.1_doc_52_1274794243#7_2564847343',
    'url': 'https://www.sociologygroup.com/industrial-revolution/',
    'title': 'Industrial Revolution: Causes, Impact and Overview',
    'headings': 'Industrial Revolution: Causes, Impact and Overview\nIndustrial Revolution: Causes, Impact and Overview\nTable of Contents\nHOW DID THE INDUSTRIAL REVOLUTION START\nThe impacts of the Industrial Revolution\nIMPACT ON TECHNOLOGY\nIMPACT ON ECONOMY\nIMPACT ON SOCIETY\nIMPACT ON INDIAN SOCIETY\nEMERGENCE OF SOCIOLOGY AS A DISCIPLINE\nAbout Meera\n',
    'segment': 'It also started agricultural trading with other countries of the continent, thus leading the country into a better financial position. The rise in population also meant an increase in demand for different other goods too. The country now was demanded to produce more output from the textile industry. This led to the need for more advancement in the textile industry of Britain. The advancements that thereby occurred in the textile industry turned out to be the chief reason for the industrial revolution. Through inventions like that of ‘Flying shuttle’ and ‘Spinning Jenny’, the textile industry of Britain became immensely advanced. The increase in population gradually led to the need for more employment. Peasant who earlier worked in rural fields thus started enclosure movement, migrating to cities in search of job. As urban centres could offer better living and employment conditions, the number of people migrating to cities saw an increase, thus leading to urbanization. With better labour force and mechanization, factories grew.',
    'start_char': 3926,
    'end_char': 4968
},
{
    'docid': 'msmarco_v2.1_doc_00_378699409#2_708658780',
    'url': 'http://apworldipedia.com/index.php?title=AP_Worldipedia',
    'title': 'AP Worldipedia - AP Worldipedia',
    'headings': 'AP Worldipedia\nAP Worldipedia\nAP World History: Modern: Course Content\n1200 to 1450\n1450 to 1750\n1750 to 1900\nThe Legacy (old) Course\nHow to Write Articles\n',
    'segment': 'Causes and Events from 1450 to 1750\nTopic 4.3 The Columbian Exchange\nTopic 4.4 Maritime Empires Established\nTopic 4.5 Maritime Empires Maintained and Developed\nTopic 4.6 Internal and External Challenges to State Power from 1450 to 1750\nTopic 4.7 Changing Social Hierarchies 1450 to 1750\n1750 to 1900\n\nUnit 5 Revolutions\nTopic 5.1 The Enlightenment\nTopic 5.2 Nationalism and Revolutions\nTopic 5.3 Industrial Revolution Begins\nTopic 5.4 Industrialization Spreads\nTopic 5.5 Technology of the Industrial Age\nTopic 5.6 Industrialization: Government’s Role\nTopic 5.7 Economic Developments and Innovations in the Industrial Age\nTopic 5.8 Reactions to the Industrial Economy\nTopic 5.9 Society and the Industrial Age\n\nUnit 6 Consequences of Industrialization\nTopic 4.1 Technological Innovations from 1450 to 1750\nTopic 4.2 Exploration: Causes and Events from 1450 to 1750\nTopic 4.3 The Columbian Exchange\nTopic 4.4 Maritime Empires Established\nTopic 4.5 Maritime Empires Maintained and Developed\nTopic 4.6 Internal and External Challenges to State Power from 1450 to 1750\nTopic 4.7 Changing Social Hierarchies 1450 to 1750\nThe Legacy (old) Course\n\nPeriod 1: 8000 BCE to 600 BCE\nKey Concept 1.1 Big Geography and the Peopling of the Earth\nKey Concept 1.2 The Neolithic Revolution and Early Agricultural Societies\nKey Concept 1.3 The Development and Interaction of Early Agricultural, Pastoral and Urban Societies\n\nPeriod 4: 1450 to 1750\nKey Concept 4.1 Globalizing Networks of Communication and Exchange\nKey Concept 4.2 New Forms of Social Organization and Modes of Production\nKey Concept 4.3 State Consolidation and Imperial Expansion\n\nPeriod 2: 600 CE to 600 CE\nKey Concept 2.1 The Development and Codification of Religious and Cultural Traditions\nKey Concept 2.2 The Development of States and Empires\nKey Concept 2.3 Emergence of Transregional Networks of Communication and Exchange\n\nPeriod 5: 1750 to 1900\nKey Concept 5.1 Industrialization and Global Capitalism\nKey Concept 5.2 Imperialism and Nation-State Formation\nKey Concept 5.3 Nationalism, Revolution, and Reform\nKey Concept 5.4 Global Migration\n\nPeriod 3: 600 to 1450\nKey Concept 3.1 Expansion and Intensification of Communication and Exchange Networks\nKey Concept 3.2 Continuity and Innovation of State Forms and Their Interactions\nKey Concept 3.3 Increased Economic Productive Capacity and its Consequences\n\nPeriod 6: 1900 to Present\nKey Concept 6.1 Science and the Environment\nKey Concept 6.2 Global Conflicts and Their Consequences\nKey Concept 6.3 New Conceptualizations of Global Economy, Society, and Culture\nHow to Write Articles\nHow to Write in WikiText\nHow to put an Image in your Article\nGrading Rubric for Writing Articles\nNote: the designations "AP" and "Advanced Placement are property of the College Board which does not endorse this website or have any connection to it.',
    'start_char': 1376,
    'end_char': 4212
},
...
```

### Output Format (Ranked Results)
Participants should provide their output in the standard TREC format containing top-k=`100` MS MARCO v2.1 segments as TSV: <`r_output_trec_rag_2025.tsv`> for each individual topic. Each set of ranked results for a set of topics appears in a single file. We will take a maximum of 100 results from each participant, more than 100 results will be truncated. Each line of this file contains six whitespace-separated entries:
- Topic ID (topic identifier taken from `trec_rag_2025_queries.jsonl`)
- The fixed string “Q0”
- Segment ID (from the docid field in `msmarco_v2.1_doc_segmented_XX.json.gz`)
- Rank (which is the rank of the segment retrieved)
- Score (integer or float that generated the ranking. This score must be in non-increasing order)
- Run ID (where you mention the ID of the run you are submitting)


```bash
...
# Example of how to return the top-100 qrels
1 Q0 msmarco_v2.1_doc_16_1041913392#3_1268938142 1 0.613857 my-run
1 Q0 msmarco_v2.1_doc_14_1198634226#9_2470404444 2 0.606288 my-run
1 Q0 msmarco_v2.1_doc_12_201312571#0_394394285 3 0.605989 my-run
1 Q0 msmarco_v2.1_doc_02_1169633399#2_1963227104 4 0.604151 my-run
1 Q0 msmarco_v2.1_doc_23_947922085#6_2108546861 5 0.596849 my-run
1 Q0 msmarco_v2.1_doc_23_564615817#13_1256293300 6 0.596674 my-run
1 Q0 msmarco_v2.1_doc_20_59107962#5_138816780 7 0.593601 my-run
1 Q0 msmarco_v2.1_doc_24_1126649978#7_2394434427 8 0.590953 my-run
1 Q0 msmarco_v2.1_doc_12_201312571#1_394396180 9 0.590736 my-run
1 Q0 msmarco_v2.1_doc_23_564615817#12_1256290771 10 0.590155 my-run
1 Q0 msmarco_v2.1_doc_13_730347647#3_1661787859 11 0.590002 my-run
1 Q0 msmarco_v2.1_doc_03_952676544#10_1612297487 12 0.589952 my-run
1 Q0 msmarco_v2.1_doc_02_1708666011#1_2905243606 13 0.589917 my-run
1 Q0 msmarco_v2.1_doc_29_6222783#1_12232334 14 0.589259 my-run
1 Q0 msmarco_v2.1_doc_03_1565360904#14_2631260538 15 0.588983 my-run
1 Q0 msmarco_v2.1_doc_16_339852969#2_601767683 16 0.588766 my-run
1 Q0 msmarco_v2.1_doc_05_1682672492#12_3232855509 17 0.588633 my-run
1 Q0 msmarco_v2.1_doc_24_1126649978#8_2394436421 18 0.588606 my-run
1 Q0 msmarco_v2.1_doc_03_952487890#11_1612181372 19 0.587185 my-run
1 Q0 msmarco_v2.1_doc_24_1132995963#0_2408027424 20 0.587181 my-run
...
```

## Augmented Generation Task (AG)

The Augmented Generation task emulates the modern-day RAG task to return the summarized answer ground based on the information available in the pre-determined list of top-k segments provided to the participant.  Participating systems will receive a list of topics, MS MARCO V2.1 segment collection and the ranked list of the top-k relevant segments for each individual topic. The topics provided will be non-factoid and require long-form answer generation.

> The AG track is for the NLP audience, focused on the generation output and quality. We provide the top-k retrieved segments, which allows the participants to focus on the answer generation quality, by grounding on the set of chunks of segments, and generate an informative & summarized answer.

### Input Format (Topics)

List of queries as topics as JSONL: <`trec_rag_2025_queries.jsonl`>, with each line containing the narrative_id and a 2-3 sentence long description of the topic.

```bash
# Example of `trec_rag_2025_queries.jsonl`
...
[
    {
        "id": "1",
        "narrative": "I'm trying to understand how the Industrial Revolution began, what caused it, and how it changed societies, economies, and populations in different countries. I'm also interested in the roles of key figures like Henry Ford, the impact of technological advancements, and how industrialization connects to topics like urbanization, migration, and modern innovations such as robotics and extended reality."
    },
    {
        "id": "2",
        "narrative": "I'm trying to understand how prisons operate, including issues like inmate rights, rehabilitation, voting, and the impact of race and profit motives on incarceration. Can you explain how correctional facilities address mental health, discipline, and recidivism, and also discuss the ethical and legal challenges inmates face?"
    }
]
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
    'docid': 'msmarco_v2.1_doc_52_1274794243#7_2564847343',
    'url': 'https://www.sociologygroup.com/industrial-revolution/',
    'title': 'Industrial Revolution: Causes, Impact and Overview',
    'headings': 'Industrial Revolution: Causes, Impact and Overview\nIndustrial Revolution: Causes, Impact and Overview\nTable of Contents\nHOW DID THE INDUSTRIAL REVOLUTION START\nThe impacts of the Industrial Revolution\nIMPACT ON TECHNOLOGY\nIMPACT ON ECONOMY\nIMPACT ON SOCIETY\nIMPACT ON INDIAN SOCIETY\nEMERGENCE OF SOCIOLOGY AS A DISCIPLINE\nAbout Meera\n',
    'segment': 'It also started agricultural trading with other countries of the continent, thus leading the country into a better financial position. The rise in population also meant an increase in demand for different other goods too. The country now was demanded to produce more output from the textile industry. This led to the need for more advancement in the textile industry of Britain. The advancements that thereby occurred in the textile industry turned out to be the chief reason for the industrial revolution. Through inventions like that of ‘Flying shuttle’ and ‘Spinning Jenny’, the textile industry of Britain became immensely advanced. The increase in population gradually led to the need for more employment. Peasant who earlier worked in rural fields thus started enclosure movement, migrating to cities in search of job. As urban centres could offer better living and employment conditions, the number of people migrating to cities saw an increase, thus leading to urbanization. With better labour force and mechanization, factories grew.',
    'start_char': 3926,
    'end_char': 4968
},
{
    'docid': 'msmarco_v2.1_doc_00_378699409#2_708658780',
    'url': 'http://apworldipedia.com/index.php?title=AP_Worldipedia',
    'title': 'AP Worldipedia - AP Worldipedia',
    'headings': 'AP Worldipedia\nAP Worldipedia\nAP World History: Modern: Course Content\n1200 to 1450\n1450 to 1750\n1750 to 1900\nThe Legacy (old) Course\nHow to Write Articles\n',
    'segment': 'Causes and Events from 1450 to 1750\nTopic 4.3 The Columbian Exchange\nTopic 4.4 Maritime Empires Established\nTopic 4.5 Maritime Empires Maintained and Developed\nTopic 4.6 Internal and External Challenges to State Power from 1450 to 1750\nTopic 4.7 Changing Social Hierarchies 1450 to 1750\n1750 to 1900\n\nUnit 5 Revolutions\nTopic 5.1 The Enlightenment\nTopic 5.2 Nationalism and Revolutions\nTopic 5.3 Industrial Revolution Begins\nTopic 5.4 Industrialization Spreads\nTopic 5.5 Technology of the Industrial Age\nTopic 5.6 Industrialization: Government’s Role\nTopic 5.7 Economic Developments and Innovations in the Industrial Age\nTopic 5.8 Reactions to the Industrial Economy\nTopic 5.9 Society and the Industrial Age\n\nUnit 6 Consequences of Industrialization\nTopic 4.1 Technological Innovations from 1450 to 1750\nTopic 4.2 Exploration: Causes and Events from 1450 to 1750\nTopic 4.3 The Columbian Exchange\nTopic 4.4 Maritime Empires Established\nTopic 4.5 Maritime Empires Maintained and Developed\nTopic 4.6 Internal and External Challenges to State Power from 1450 to 1750\nTopic 4.7 Changing Social Hierarchies 1450 to 1750\nThe Legacy (old) Course\n\nPeriod 1: 8000 BCE to 600 BCE\nKey Concept 1.1 Big Geography and the Peopling of the Earth\nKey Concept 1.2 The Neolithic Revolution and Early Agricultural Societies\nKey Concept 1.3 The Development and Interaction of Early Agricultural, Pastoral and Urban Societies\n\nPeriod 4: 1450 to 1750\nKey Concept 4.1 Globalizing Networks of Communication and Exchange\nKey Concept 4.2 New Forms of Social Organization and Modes of Production\nKey Concept 4.3 State Consolidation and Imperial Expansion\n\nPeriod 2: 600 CE to 600 CE\nKey Concept 2.1 The Development and Codification of Religious and Cultural Traditions\nKey Concept 2.2 The Development of States and Empires\nKey Concept 2.3 Emergence of Transregional Networks of Communication and Exchange\n\nPeriod 5: 1750 to 1900\nKey Concept 5.1 Industrialization and Global Capitalism\nKey Concept 5.2 Imperialism and Nation-State Formation\nKey Concept 5.3 Nationalism, Revolution, and Reform\nKey Concept 5.4 Global Migration\n\nPeriod 3: 600 to 1450\nKey Concept 3.1 Expansion and Intensification of Communication and Exchange Networks\nKey Concept 3.2 Continuity and Innovation of State Forms and Their Interactions\nKey Concept 3.3 Increased Economic Productive Capacity and its Consequences\n\nPeriod 6: 1900 to Present\nKey Concept 6.1 Science and the Environment\nKey Concept 6.2 Global Conflicts and Their Consequences\nKey Concept 6.3 New Conceptualizations of Global Economy, Society, and Culture\nHow to Write Articles\nHow to Write in WikiText\nHow to put an Image in your Article\nGrading Rubric for Writing Articles\nNote: the designations "AP" and "Advanced Placement are property of the College Board which does not endorse this website or have any connection to it.',
    'start_char': 1376,
    'end_char': 4212
},
...
```

### Input Format (Ranked Results)

Top-100 retrieved segments for each individual topic using our baseline retrieval system on the MS MARCO v2.1 segment collection: <`baseline_r_out.tsv`>.
We will provide a maximum of 100 segments for each individual topic. 
This file has the same format as the output file for the retrieval task.

```bash
- Topic ID (taken from `trec_rag_2025_queries.jsonl`)
- The fixed string “Q0”
- Segment ID (from the docid field in `msmarco_v2.1_doc_segmented_XX.json.gz`)
- Rank (which is the rank of the segment retrieved)
- Score (integer or float that generated the ranking. This score must be in descending, non-increasing order)
- Run ID (where you mention the ID of the run you are submitting)
```

We will additionally provide reranker requests JSONL file, <`baseline_r_out.jsonl``>, described at the end of the section [here](https://github.com/castorini/ragnarok/blob/main/docs/rag24.md#retrieval---bm25), where each line is a JSON object with the following fields:

```python
{
    "query": {
        "narrative_id": 1, # topic_id
        "narrative": "I'm trying to understand how the Industrial Revolution began, what caused it, and how it changed societies, economies, and populations in different countries. I'm also interested in the roles of key figures like Henry Ford, the impact of technological advancements, and how industrialization connects to topics like urbanization, migration, and modern innovations such as robotics and extended reality." # narrative
    }, 
    "candidates": [
        {
            "docid": "msmarco_v2.1_doc_...",
            "score": 18.2876,
            "doc": 
            {
                "url": "...",
                "title": "...",
                "headings": "...",
                "segment": "...",
                "start_char": 1234,
                "end_char": 4567
            }
        },
        {
            ...
        }
    ]
}
```

Providing the url, title, headings, segment, start_char, and end_char fields for each candidate segment will help participants with limitations in downloading the entire MS MARCO v2.1 segment collection, to still get to participate in the AG task.

### Output Format (AG Output)

Participants should provide their output in the standard JSONL format containing the following JSON information as <`ag_output_trec_rag_2025.jsonl`> for each individual topic. The final RAG answer should provided in the following JSON format. Each line of this JSONL file contains the following entries:

Format 1:

- team_id (string) containing your team tag
- run_id (string) containing your run tag
- type (string) run type, manual or automatic
- narrative_id (string) from the narrative_id taken from `trec_rag_2025_queries.jsonl`
- narrative (string) the 2-3 sentence long description of the topic taken from `trec_rag_2025_queries.jsonl`
- references (array) containing the ranked list of top-k segment IDs from the retrieval stage (a maximum of only 20 segments is allowed)
- response_length (integer) containing the total words present in the overall RAG response.
- answer (array) containing the list of sentences and citations from the `references` list. The `text` field contains the response and `citations` field contains the (zero-indexed) reference of the segment from the `references` list (sorted from highest to lowest citation support).

```python
{
    "metadata": {
        "team_id": "my-awesome-team",
        "run_id": "my-awesome-run",
        "type": "automatic",
    },
    "narrative_id": 1, # topic_id
    "narrative": "I'm trying to understand how the Industrial Revolution began, what caused it, and how it changed societies, economies, and populations in different countries. I'm also interested in the roles of key figures like Henry Ford, the impact of technological advancements, and how industrialization connects to topics like urbanization, migration, and modern innovations such as robotics and extended reality.", # query
    "references": [ # top-k segments returned used from the retrieval step. We have k equals to 20 segments for this example.
        'msmarco_v2.1_doc_16_1041913392#3_1268938142',
        'msmarco_v2.1_doc_14_1198634226#9_2470404444',
        'msmarco_v2.1_doc_12_201312571#0_394394285',
        'msmarco_v2.1_doc_02_1169633399#2_1963227104',
        'msmarco_v2.1_doc_23_947922085#6_2108546861',
        'msmarco_v2.1_doc_23_564615817#13_1256293300',
        'msmarco_v2.1_doc_20_59107962#5_138816780',
        'msmarco_v2.1_doc_24_1126649978#7_2394434427',
        'msmarco_v2.1_doc_12_201312571#1_394396180',
        'msmarco_v2.1_doc_23_564615817#12_1256290771',
        'msmarco_v2.1_doc_13_730347647#3_1661787859',
        'msmarco_v2.1_doc_03_952676544#10_1612297487',
        'msmarco_v2.1_doc_02_1708666011#1_2905243606',
        'msmarco_v2.1_doc_29_6222783#1_12232334',
        'msmarco_v2.1_doc_03_1565360904#14_2631260538',
        'msmarco_v2.1_doc_16_339852969#2_601767683',
        'msmarco_v2.1_doc_05_1682672492#12_3232855509',
        'msmarco_v2.1_doc_24_1126649978#8_2394436421',
        'msmarco_v2.1_doc_03_952487890#11_1612181372',
        'msmarco_v2.1_doc_24_1132995963#0_2408027424'
        ]
    "response_length": 145, 
    "answer": [ # RAG answer broken into sentences with each answer sentence grounding information from the index mentioned in references.
            {"text": "The Industrial Revolution began in Britain in the mid-18th century, fueled by its abundant coal and iron resources, a large labor force, and access to capital and global trade networks.", "citations": [0, 8, 15]}, 
            {"text": "Technological innovations like the steam engine, telegraph, spinning jenny, and power loom dramatically increased productivity and reshaped industries.", "citations": [8, 16]}, 
            {"text": "These technological breakthroughs increased productivity and transformed global transportation and communication, fueling trade and migration across continents.", "citations": [6, 12]}, 
            {"text": "As fewer people were needed on farms due to mechanization, populations moved to cities for factory jobs, driving rapid urbanization and demographic shifts.", "citations": [5, 13]}, 
            {"text": "This urban migration led to crowded living conditions, labor exploitation, and child labor, prompting the rise of labor unions and demands for reforms.", "citations": [9, 14]}, 
            {"text": "Figures like Henry Ford played a transformative role during the Second Industrial Revolution by introducing the assembly line, which dramatically boosted production efficiency.", "citations": [16, 18]}, 
            {"text": "The technological foundation laid during this era continues to influence the modern world through innovations like robotics, automation, and immersive technologies.", "citations": [11, 17]}
        ]
}
```

Format 2 (similar to other tracks):

- team_id (string) containing your team tag
- run_id (string) containing your run tag
- type (string) run type, manual or automatic
- narrative_id (string) from the narrative_id taken from `trec_rag_2025_queries.jsonl`
- narrative (string) the 2-3 sentence long description of the topic taken from `trec_rag_2025_queries.jsonl`
- response_length (integer) containing the total words present in the overall RAG response.
- answer (array) containing the list of sentences and citations from the `references` list. The `text` field contains the response and `citations` field contains the ID of the segment (sorted from highest to lowest citation support).

```python
{
    "metadata": {
        "team_id": "my-awesome-team",
        "run_id": "my-awesome-run",
        "type": "automatic",
    },
    "narrative_id": 1, # topic_id
    "narrative": "I'm trying to understand how the Industrial Revolution began, what caused it, and how it changed societies, economies, and populations in different countries. I'm also interested in the roles of key figures like Henry Ford, the impact of technological advancements, and how industrialization connects to topics like urbanization, migration, and modern innovations such as robotics and extended reality.", # query
    "response_length": 145, 
    "answer": [ # RAG answer broken into sentences with each answer sentence grounding information from the index mentioned in references.
            {"text": "The Industrial Revolution began in Britain in the mid-18th century, fueled by its abundant coal and iron resources, a large labor force, and access to capital and global trade networks.", 
            "citations": ['msmarco_v2.1_doc_16_1041913392#3_1268938142', 'msmarco_v2.1_doc_12_201312571#1_394396180', 'msmarco_v2.1_doc_16_339852969#2_601767683']}, 
            {"text": "Technological innovations like the steam engine, telegraph, spinning jenny, and power loom dramatically increased productivity and reshaped industries.", 
            "citations": ['msmarco_v2.1_doc_12_201312571#1_394396180', 'msmarco_v2.1_doc_05_1682672492#12_3232855509']}, 
            {"text": "These technological breakthroughs increased productivity and transformed global transportation and communication, fueling trade and migration across continents.", 
            "citations": ['msmarco_v2.1_doc_20_59107962#5_138816780', 'msmarco_v2.1_doc_02_1708666011#1_2905243606']}, 
            {"text": "As fewer people were needed on farms due to mechanization, populations moved to cities for factory jobs, driving rapid urbanization and demographic shifts.", 
            "citations": ['msmarco_v2.1_doc_23_564615817#13_1256293300', 'msmarco_v2.1_doc_29_6222783#1_12232334']}, 
            {"text": "This urban migration led to crowded living conditions, labor exploitation, and child labor, prompting the rise of labor unions and demands for reforms.", 
            "citations": ['msmarco_v2.1_doc_23_564615817#12_1256290771', 'msmarco_v2.1_doc_03_1565360904#14_2631260538']}, 
            {"text": "Figures like Henry Ford played a transformative role during the Second Industrial Revolution by introducing the assembly line, which dramatically boosted production efficiency.", 
            "citations": ['msmarco_v2.1_doc_05_1682672492#12_3232855509', 'msmarco_v2.1_doc_03_952487890#11_1612181372']}, 
            {"text": "The technological foundation laid during this era continues to influence the modern world through innovations like robotics, automation, and immersive technologies.", 
            "citations": ['msmarco_v2.1_doc_03_952676544#10_1612297487', 'msmarco_v2.1_doc_24_1126649978#8_2394436421']}
        ]
}
```

## Retrieval-Augmented Generation Task (RAG)

- **Given**: Participants will be provided a list of topics and both the MS MARCO v2.1 document and MS MARCO v2.1 segment collections. 
- **Task**: Return the summarized answer and ground based on information which you can either the MS MARCO v2.1 document or segment collection. Develop your own retrieval system to fetch relevant information from the MS MARCO v2.1 segment/document collection. You can use either our pre-determined segment collection or incorporate your own **chunking** technique with the MS MARCO v2.1 document collection. For evaluation, we ask each participant to map their chunk of segments with MS MARCO v2.1 segment collections.
- **Notes**: The RAG track is a mixture of above (R) and (AG) tracks. This setup mimics best the industrial RAG setup for the NLP+IR audience. We evaluate the summarized answer in multiple ways incorporating both grounding and evaluating fluency of the generated output.

### Input Format (Topics)

List of queries as topics as JSONL: <`trec_rag_2025_queries.jsonl`>, with each line containing the narrative_id and 2-3 sentence long description of the topic.

```bash
# Example of `trec_rag_2025_queries.jsonl`
...
[
    {
        "id": "1",
        "narrative": "I'm trying to understand how the Industrial Revolution began, what caused it, and how it changed societies, economies, and populations in different countries. I'm also interested in the roles of key figures like Henry Ford, the impact of technological advancements, and how industrialization connects to topics like urbanization, migration, and modern innovations such as robotics and extended reality."
    },
    {
        "id": "2",
        "narrative": "I'm trying to understand how prisons operate, including issues like inmate rights, rehabilitation, voting, and the impact of race and profit motives on incarceration. Can you explain how correctional facilities address mental health, discipline, and recidivism, and also discuss the ethical and legal challenges inmates face?"
    }
]
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
  "docid": "msmarco_v2.1_doc_00_378699409",
  "url": "http://apworldipedia.com/index.php?title=AP_Worldipedia",
  "title": "AP Worldipedia - AP Worldipedia",
  "headings": "AP Worldipedia\nAP Worldipedia\nAP World History: Modern: Course Content\n1200 to 1450\n1450 to 1750\n1750 to 1900\nThe Legacy (old) Course\nHow to Write Articles\n",
  "body": "AP Worldipedia - AP Worldipedia\nAP Worldipedia\nFrom AP Worldipedia\nJump to navigation Jump to search\nWelcome to AP Worldipedia, the free encyclopedia covering the content for Advanced Placement World History. Below are the topics on which this course is based. Each has been filled out into a narrative text with illustrative media. Although they do not necessarily follow the chronological order in which the content will be taught in class, they should be useful in summarizing the basics of the course. All questions on the AP World History test in May are built on the topics you see listed on this website.\nAP World History: Modern: Course Content\n1200 to 1450\n\nUnit 1 The Global Tapestry\nTopic 1.1 Developments in East Asia 1200 to 1450\nTopic 1.2 Developments in Dar al-Islam 1200 to 1450\nTopic 1.3 Developments in South and Southeast Asia 1200 to 1450\nTopic 1.4 State Building in the Americas\nTopic 1.5 State Building in Africa\n\nUnit 2 Networks of Exchange\nTopic 2.1 The Silk Roads\nTopic 2.2 The Mongol Empire and the Making of the Modern World\nTopic 2.3 Exchange in the Indian Ocean\nTopic 2.4 Trans-Saharan Trade Routes\n1450 to 1750\n\nUnit 3 Land-Based Empires\nTopic 3.1 Empires Expand\nTopic 3.2 Empires: Administration\nTopic 3.3 Empires: Belief Systems\n\nUnit 4 Transoceonic Interconnections\nTopic 4.1 Technological Innovations from 1450 to 1750\nTopic 4.2 Exploration: Causes and Events from 1450 to 1750\nTopic 4.3 The Columbian Exchange\nTopic 4.4 Maritime Empires Established\nTopic 4.5 Maritime Empires Maintained and Developed\nTopic 4.6 Internal and External Challenges to State Power from 1450 to 1750\nTopic 4.7 Changing Social Hierarchies 1450 to 1750\n1750 to 1900\n\nUnit 5 Revolutions\nTopic 5.1 The Enlightenment\nTopic 5.2 Nationalism and Revolutions\nTopic 5.3 Industrial Revolution Begins\nTopic 5.4 Industrialization Spreads\nTopic 5.5 Technology of the Industrial Age\nTopic 5.6 Industrialization: Government\u2019s Role\nTopic 5.7 Economic Developments and Innovations in the Industrial Age\nTopic 5.8 Reactions to the Industrial Economy\nTopic 5.9 Society and the Industrial Age\n\nUnit 6 Consequences of Industrialization\nTopic 4.1 Technological Innovations from 1450 to 1750\nTopic 4.2 Exploration: Causes and Events from 1450 to 1750\nTopic 4.3 The Columbian Exchange\nTopic 4.4 Maritime Empires Established\nTopic 4.5 Maritime Empires Maintained and Developed\nTopic 4.6 Internal and External Challenges to State Power from 1450 to 1750\nTopic 4.7 Changing Social Hierarchies 1450 to 1750\nThe Legacy (old) Course\n\nPeriod 1: 8000 BCE to 600 BCE\nKey Concept 1.1 Big Geography and the Peopling of the Earth\nKey Concept 1.2 The Neolithic Revolution and Early Agricultural Societies\nKey Concept 1.3 The Development and Interaction of Early Agricultural, Pastoral and Urban Societies\n\nPeriod 4: 1450 to 1750\nKey Concept 4.1 Globalizing Networks of Communication and Exchange\nKey Concept 4.2 New Forms of Social Organization and Modes of Production\nKey Concept 4.3 State Consolidation and Imperial Expansion\n\nPeriod 2: 600 CE to 600 CE\nKey Concept 2.1 The Development and Codification of Religious and Cultural Traditions\nKey Concept 2.2 The Development of States and Empires\nKey Concept 2.3 Emergence of Transregional Networks of Communication and Exchange\n\nPeriod 5: 1750 to 1900\nKey Concept 5.1 Industrialization and Global Capitalism\nKey Concept 5.2 Imperialism and Nation-State Formation\nKey Concept 5.3 Nationalism, Revolution, and Reform\nKey Concept 5.4 Global Migration\n\nPeriod 3: 600 to 1450\nKey Concept 3.1 Expansion and Intensification of Communication and Exchange Networks\nKey Concept 3.2 Continuity and Innovation of State Forms and Their Interactions\nKey Concept 3.3 Increased Economic Productive Capacity and its Consequences\n\nPeriod 6: 1900 to Present\nKey Concept 6.1 Science and the Environment\nKey Concept 6.2 Global Conflicts and Their Consequences\nKey Concept 6.3 New Conceptualizations of Global Economy, Society, and Culture\nHow to Write Articles\nHow to Write in WikiText\nHow to put an Image in your Article\nGrading Rubric for Writing Articles\nNote: the designations \"AP\" and \"Advanced Placement are property of the College Board which does not endorse this website or have any connection to it.\nRetrieved from \" http://apworldipedia.com/index.php?title=AP_Worldipedia&oldid=5009 \""
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
    'docid': 'msmarco_v2.1_doc_52_1274794243#7_2564847343',
    'url': 'https://www.sociologygroup.com/industrial-revolution/',
    'title': 'Industrial Revolution: Causes, Impact and Overview',
    'headings': 'Industrial Revolution: Causes, Impact and Overview\nIndustrial Revolution: Causes, Impact and Overview\nTable of Contents\nHOW DID THE INDUSTRIAL REVOLUTION START\nThe impacts of the Industrial Revolution\nIMPACT ON TECHNOLOGY\nIMPACT ON ECONOMY\nIMPACT ON SOCIETY\nIMPACT ON INDIAN SOCIETY\nEMERGENCE OF SOCIOLOGY AS A DISCIPLINE\nAbout Meera\n',
    'segment': 'It also started agricultural trading with other countries of the continent, thus leading the country into a better financial position. The rise in population also meant an increase in demand for different other goods too. The country now was demanded to produce more output from the textile industry. This led to the need for more advancement in the textile industry of Britain. The advancements that thereby occurred in the textile industry turned out to be the chief reason for the industrial revolution. Through inventions like that of ‘Flying shuttle’ and ‘Spinning Jenny’, the textile industry of Britain became immensely advanced. The increase in population gradually led to the need for more employment. Peasant who earlier worked in rural fields thus started enclosure movement, migrating to cities in search of job. As urban centres could offer better living and employment conditions, the number of people migrating to cities saw an increase, thus leading to urbanization. With better labour force and mechanization, factories grew.',
    'start_char': 3926,
    'end_char': 4968
},
{
    'docid': 'msmarco_v2.1_doc_00_378699409#2_708658780',
    'url': 'http://apworldipedia.com/index.php?title=AP_Worldipedia',
    'title': 'AP Worldipedia - AP Worldipedia',
    'headings': 'AP Worldipedia\nAP Worldipedia\nAP World History: Modern: Course Content\n1200 to 1450\n1450 to 1750\n1750 to 1900\nThe Legacy (old) Course\nHow to Write Articles\n',
    'segment': 'Causes and Events from 1450 to 1750\nTopic 4.3 The Columbian Exchange\nTopic 4.4 Maritime Empires Established\nTopic 4.5 Maritime Empires Maintained and Developed\nTopic 4.6 Internal and External Challenges to State Power from 1450 to 1750\nTopic 4.7 Changing Social Hierarchies 1450 to 1750\n1750 to 1900\n\nUnit 5 Revolutions\nTopic 5.1 The Enlightenment\nTopic 5.2 Nationalism and Revolutions\nTopic 5.3 Industrial Revolution Begins\nTopic 5.4 Industrialization Spreads\nTopic 5.5 Technology of the Industrial Age\nTopic 5.6 Industrialization: Government’s Role\nTopic 5.7 Economic Developments and Innovations in the Industrial Age\nTopic 5.8 Reactions to the Industrial Economy\nTopic 5.9 Society and the Industrial Age\n\nUnit 6 Consequences of Industrialization\nTopic 4.1 Technological Innovations from 1450 to 1750\nTopic 4.2 Exploration: Causes and Events from 1450 to 1750\nTopic 4.3 The Columbian Exchange\nTopic 4.4 Maritime Empires Established\nTopic 4.5 Maritime Empires Maintained and Developed\nTopic 4.6 Internal and External Challenges to State Power from 1450 to 1750\nTopic 4.7 Changing Social Hierarchies 1450 to 1750\nThe Legacy (old) Course\n\nPeriod 1: 8000 BCE to 600 BCE\nKey Concept 1.1 Big Geography and the Peopling of the Earth\nKey Concept 1.2 The Neolithic Revolution and Early Agricultural Societies\nKey Concept 1.3 The Development and Interaction of Early Agricultural, Pastoral and Urban Societies\n\nPeriod 4: 1450 to 1750\nKey Concept 4.1 Globalizing Networks of Communication and Exchange\nKey Concept 4.2 New Forms of Social Organization and Modes of Production\nKey Concept 4.3 State Consolidation and Imperial Expansion\n\nPeriod 2: 600 CE to 600 CE\nKey Concept 2.1 The Development and Codification of Religious and Cultural Traditions\nKey Concept 2.2 The Development of States and Empires\nKey Concept 2.3 Emergence of Transregional Networks of Communication and Exchange\n\nPeriod 5: 1750 to 1900\nKey Concept 5.1 Industrialization and Global Capitalism\nKey Concept 5.2 Imperialism and Nation-State Formation\nKey Concept 5.3 Nationalism, Revolution, and Reform\nKey Concept 5.4 Global Migration\n\nPeriod 3: 600 to 1450\nKey Concept 3.1 Expansion and Intensification of Communication and Exchange Networks\nKey Concept 3.2 Continuity and Innovation of State Forms and Their Interactions\nKey Concept 3.3 Increased Economic Productive Capacity and its Consequences\n\nPeriod 6: 1900 to Present\nKey Concept 6.1 Science and the Environment\nKey Concept 6.2 Global Conflicts and Their Consequences\nKey Concept 6.3 New Conceptualizations of Global Economy, Society, and Culture\nHow to Write Articles\nHow to Write in WikiText\nHow to put an Image in your Article\nGrading Rubric for Writing Articles\nNote: the designations "AP" and "Advanced Placement are property of the College Board which does not endorse this website or have any connection to it.',
    'start_char': 1376,
    'end_char': 4212
},
...
```

### Output Format (RAG Output)
Output containing the following JSON information as <`rag_output_trec_rag_2025.jsonl`>. You can feel free to use the document collection with your own segmentation choice of yours, however, to make this collection reusable, we require the participant to map their custom chunked segments with segments available from MS MARCO V2.1 segment collection. Each line of this JSONL file contains the following entries:

Format 1:

- team_id (string) containing your team tag
- run_id (string) containing your run tag
- type (string) run type, manual or automatic
- narrative_id (string) from the narrative_id taken from `trec_rag_2025_queries.jsonl`
- narrative (string) the 2-3 sentence long description of the topic taken from `trec_rag_2025_queries.jsonl`
- references (array) containing the ranked list of top-k segment IDs from the retrieval stage (a maximum of only 20 segments is allowed)
- response_length (integer) containing the total words present in the overall RAG response.
- answer (array) containing the list of sentences and citations from the `references` list. The `text` field contains the response and `citations` field contains the (zero-indexed) reference of the segment from the `references` list (sorted from highest to lowest citation support).

```python
{
    "metadata": {
        "team_id": "my-awesome-team",
        "run_id": "my-awesome-run",
        "type": "automatic",
    },
    "narrative_id": 1, # topic_id
    "narrative": "I'm trying to understand how the Industrial Revolution began, what caused it, and how it changed societies, economies, and populations in different countries. I'm also interested in the roles of key figures like Henry Ford, the impact of technological advancements, and how industrialization connects to topics like urbanization, migration, and modern innovations such as robotics and extended reality.", # query
    "references": [ # top-k segments returned used from the retrieval step. We have k equals to 20 segments for this example.
        'msmarco_v2.1_doc_16_1041913392#3_1268938142',
        'msmarco_v2.1_doc_14_1198634226#9_2470404444',
        'msmarco_v2.1_doc_12_201312571#0_394394285',
        'msmarco_v2.1_doc_02_1169633399#2_1963227104',
        'msmarco_v2.1_doc_23_947922085#6_2108546861',
        'msmarco_v2.1_doc_23_564615817#13_1256293300',
        'msmarco_v2.1_doc_20_59107962#5_138816780',
        'msmarco_v2.1_doc_24_1126649978#7_2394434427',
        'msmarco_v2.1_doc_12_201312571#1_394396180',
        'msmarco_v2.1_doc_23_564615817#12_1256290771',
        'msmarco_v2.1_doc_13_730347647#3_1661787859',
        'msmarco_v2.1_doc_03_952676544#10_1612297487',
        'msmarco_v2.1_doc_02_1708666011#1_2905243606',
        'msmarco_v2.1_doc_29_6222783#1_12232334',
        'msmarco_v2.1_doc_03_1565360904#14_2631260538',
        'msmarco_v2.1_doc_16_339852969#2_601767683',
        'msmarco_v2.1_doc_05_1682672492#12_3232855509',
        'msmarco_v2.1_doc_24_1126649978#8_2394436421',
        'msmarco_v2.1_doc_03_952487890#11_1612181372',
        'msmarco_v2.1_doc_24_1132995963#0_2408027424'
        ]
    "response_length": 145, 
    "answer": [ # RAG answer broken into sentences with each answer sentence grounding information from the index mentioned in references.
            {"text": "The Industrial Revolution began in Britain in the mid-18th century, fueled by its abundant coal and iron resources, a large labor force, and access to capital and global trade networks.", "citations": [0, 8, 15]}, 
            {"text": "Technological innovations like the steam engine, telegraph, spinning jenny, and power loom dramatically increased productivity and reshaped industries.", "citations": [8, 16]}, 
            {"text": "These technological breakthroughs increased productivity and transformed global transportation and communication, fueling trade and migration across continents.", "citations": [6, 12]}, 
            {"text": "As fewer people were needed on farms due to mechanization, populations moved to cities for factory jobs, driving rapid urbanization and demographic shifts.", "citations": [5, 13]}, 
            {"text": "This urban migration led to crowded living conditions, labor exploitation, and child labor, prompting the rise of labor unions and demands for reforms.", "citations": [9, 14]}, 
            {"text": "Figures like Henry Ford played a transformative role during the Second Industrial Revolution by introducing the assembly line, which dramatically boosted production efficiency.", "citations": [16, 18]}, 
            {"text": "The technological foundation laid during this era continues to influence the modern world through innovations like robotics, automation, and immersive technologies.", "citations": [11, 17]}
        ]
}
```

Format 2 (similar to other tracks):

- team_id (string) containing your team tag
- run_id (string) containing your run tag
- type (string) run type, manual or automatic
- narrative_id (string) from the narrative_id taken from `trec_rag_2025_queries.jsonl`
- narrative (string) the 2-3 sentence long description of the topic taken from `trec_rag_2025_queries.jsonl`
- response_length (integer) containing the total words present in the overall RAG response.
- answer (array) containing the list of sentences and citations from the `references` list. The `text` field contains the response and `citations` field contains the ID of the segment (sorted from highest to lowest citation support).

```python
{
    "metadata": {
        "team_id": "my-awesome-team",
        "run_id": "my-awesome-run",
        "type": "automatic",
    },
    "narrative_id": 1, # topic_id
    "narrative": "I'm trying to understand how the Industrial Revolution began, what caused it, and how it changed societies, economies, and populations in different countries. I'm also interested in the roles of key figures like Henry Ford, the impact of technological advancements, and how industrialization connects to topics like urbanization, migration, and modern innovations such as robotics and extended reality.", # query
    "response_length": 145, 
    "answer": [ # RAG answer broken into sentences with each answer sentence grounding information from the index mentioned in references.
            {"text": "The Industrial Revolution began in Britain in the mid-18th century, fueled by its abundant coal and iron resources, a large labor force, and access to capital and global trade networks.", 
            "citations": ['msmarco_v2.1_doc_16_1041913392#3_1268938142', 'msmarco_v2.1_doc_12_201312571#1_394396180', 'msmarco_v2.1_doc_16_339852969#2_601767683']}, 
            {"text": "Technological innovations like the steam engine, telegraph, spinning jenny, and power loom dramatically increased productivity and reshaped industries.", 
            "citations": ['msmarco_v2.1_doc_12_201312571#1_394396180', 'msmarco_v2.1_doc_05_1682672492#12_3232855509']}, 
            {"text": "These technological breakthroughs increased productivity and transformed global transportation and communication, fueling trade and migration across continents.", 
            "citations": ['msmarco_v2.1_doc_20_59107962#5_138816780', 'msmarco_v2.1_doc_02_1708666011#1_2905243606']}, 
            {"text": "As fewer people were needed on farms due to mechanization, populations moved to cities for factory jobs, driving rapid urbanization and demographic shifts.", 
            "citations": ['msmarco_v2.1_doc_23_564615817#13_1256293300', 'msmarco_v2.1_doc_29_6222783#1_12232334']}, 
            {"text": "This urban migration led to crowded living conditions, labor exploitation, and child labor, prompting the rise of labor unions and demands for reforms.", 
            "citations": ['msmarco_v2.1_doc_23_564615817#12_1256290771', 'msmarco_v2.1_doc_03_1565360904#14_2631260538']}, 
            {"text": "Figures like Henry Ford played a transformative role during the Second Industrial Revolution by introducing the assembly line, which dramatically boosted production efficiency.", 
            "citations": ['msmarco_v2.1_doc_05_1682672492#12_3232855509', 'msmarco_v2.1_doc_03_952487890#11_1612181372']}, 
            {"text": "The technological foundation laid during this era continues to influence the modern world through innovations like robotics, automation, and immersive technologies.", 
            "citations": ['msmarco_v2.1_doc_03_952676544#10_1612297487', 'msmarco_v2.1_doc_24_1126649978#8_2394436421']}
        ]
}
```

## Next Steps

We encourage participants to start encoding the MS MARCO V2.1 segment corpus (120+ million) using their favourite retrieval system.
We will soon release the test topics.

We encourage the community to provide us with constructive feedback regarding any task, or require us to further clarify any task.
Please feel free to reach out to us via Twitter/Slack!

*The TREC RAG Organizers Send Their Regards.*