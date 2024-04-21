---
title: "TREC 2024 RAG Task Description (Draft)"
date: 2024-04-18T09:00:00-00:00
categories:
  - Annoucements
tags:
  - TREC 2024
  - Tasks
classes: wide
toc: false
---

We are excited to provide details on each task which will be conducted in the first year of the TREC RAG! 🎉🎉

# TASK 1: Retrieval Track (R)

- **Given**: Participants will be provided a list of topics and the complete MS MARCO V2.1 segment collection.
- **Task**: Provide back the run file containing the top relevant segments from the MS MARCO V2.1 segment collection for each individual topic. 
- **Notes**: The “R” track emulates the previous TREC-DL 2022/2023 tracks is for the IR audience, however, the main difference lies in using document segments from the MS MARCO V2.1 segment collection instead of the MS MARCO v2.0 passage collection.

## INPUT to participant

1. List of queries as topics as TSV: <`trec_rag_2024_queries.tsv`>

```bash
# Example of `trec_rag_2024_queries.tsv`
...
2027497	how often should you take your toddler to the potty when potty training
300986	how many years in jail for money laundering
835760	what is the name of the triangular region at the base of the bladder?
...
```

2. MS MARCO v2.1 segment corpus as JSONL: <`msmarco_v2.1_doc_segmented_XX.json.gz`>

```python
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

## OUTPUT from participant
Output in TREC format containing top-k=`100` MS MARCO v2.1 segments as TSV: <`r_output_trec_rag_2024.tsv`>:

```bash
...
# Example of how to return the top-k qrels
2027497 Q0 msmarco_v2.1_doc_51_766815931#2_1606878413 0.99986017 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_51_766815931#1_1606876582 0.9996673 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_51_766815931#5_1606882767 0.99931216 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_51_766815931#6_1606884302 0.99923867 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_51_766815931#3_1606879951 0.99862224 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_51_766815931#4_1606881348 0.9985786 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_37_463237391#10_984448281 0.99851626 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_51_766815931#0_1606874600 0.9980733 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_37_463237391#9_984446615 0.99794924 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_28_472446307#22_1012988885 0.99647564 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_51_766815931#7_1606885873 0.9926826 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_28_472446307#21_1012986800 0.9922143 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_29_562342450#23_1356565296 0.9852146 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_29_562342450#17_1356555947 0.9829547 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_49_418787959#7_861728734 0.97997653 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_49_418787959#6_861726964 0.9739437 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_26_680625866#7_1289507527 0.97334224 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_10_1346272776#19_2165266355 0.9732915 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_56_1491300640#3_3012150696 0.97272736 cohere-v3.0
2027497 Q0 msmarco_v2.1_doc_10_672519892#5_1260010758 0.9719925 cohere-v3.0
...
```

# TASK 2: Augmented Generation Track (AG)

- **Given**: Participants will be provided a list of topics and top-k relevant retrieved segments mapped with the MS MARCO V2.1 segment collection.
- **Task**: Return the summarized answer ground based on the information available in the pre-determined list of top-k segments provided to the participant. 
- **Notes**: The AG track is for the NLP audience, focused on the generation output and quality. We provide the top-k retrieved segments, which allows the participants to focus on the RAG generation quality, by grounding on the set of chunks of segments, and generate an informative RAG summarized answer.

## INPUT to participant
1. List of queries as topics as TSV: <`trec_rag_2024_queries.tsv`>

```bash
# Example of `trec_rag_2024_queries.tsv`
...
2027497	how often should you take your toddler to the potty when potty training
300986	how many years in jail for money laundering
835760	what is the name of the triangular region at the base of the bladder?
...
```

2. MS MARCO v2.1 segment collection as JSONL: <`msmarco_v2.1_doc_segmented_XX.json.gz`>

```python
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

3. Top-k retrieved segments using our internal retrieval system on the MS MARCO v2.1 segment collection: <`trec_rag_2024_qrels.tsv`>
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

## OUTPUT from participant
Output containing the following JSON information as <`ag_output_trec_rag_2024.jsonl`>:

```python
{
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
        "response_length": 1090, 
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

# TASK 3: Retrieval-Augmented Generation Track (RAG)

- **Given**: Participants will be provided a list of topics and both the MS MARCO v2.1 document and MS MARCO v2.1 segment collections. 
- **Task**: Return the summarized answer and ground based on information which you can either the MS MARCO v2.1 document or segment collection. Develop your own retrieval system to fetch relevant information from the MS MARCO v2.1 segment/document collection. You can use either our pre-determined segment collection or incorporate your own **chunking** technique with the MS MARCO v2.1 document collection. For evaluation, we ask each participant to map their chunk of segments with MS MARCO v2.1 segment collections.
- **Notes**: The RAG track is a mixture of above (R) and (AG) tracks. This setup mimics best the industrial RAG setup for the NLP+IR audience. We evaluate the summarized answer in multiple ways incorporating both grounding and evaluating fluency of the generated output.

## INPUT to participant

1. List of queries as topics as TSV: <`trec_rag_2024_queries.tsv`>

```bash
# Example of `trec_rag_2024_queries.tsv`
...
2027497	how often should you take your toddler to the potty when potty training
300986	how many years in jail for money laundering
835760	what is the name of the triangular region at the base of the bladder?
...
```

2. MS MARCO v2.1 Segment/Document collection: <`msmarco_v2.1_doc_segmented_XX.json.gz`>

Example from MS MARCO v2.1 Document collection:
```python
{
    'docid': 'msmarco_v2.1_doc_51_766815931',
    'url': 'https://www.romper.com/p/how-often-should-i-take-my-toddler-to-the-potty-there-are-some-guidelines-to-follow-71586', 
    'title': 'How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow', 
    'headings': 'How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nHow Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow', 
    'body': 'How Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nLife\nAshley Batz/Romper\nHow Often Should I Take My Toddler To The Potty? There Are Some Guidelines To Follow\nby Kelly Mullen-McWilliams\nJuly 22, 2017\nI don\'t know about you, but I\'m personally super pumped for that perfect day in the admittedly far-off future when I throw that last diaper away — and then throw myself a party. If you\'re currently in the midst of toilet training, I salute you, and I also know you have a lot of questions. Whether it\'s going well or not, you\'re probably wondering things like, " how often should I take my toddler to the potty ?"\nMore Like This\nVaccinated People Can Ditch Masks. Where Does That Leave Kids?\n25 Real-Life Reasons Not To Trust Older Siblings Around The Baby\nMoms To Toddlers Everywhere: This Aggression Will Not Stand, Man\nHow 20 Kids Brought The Pandemic Into Their Play Worlds\nWhat Parents Are Talking About — Delivered Straight To Your Inbox\nSubscribe\nAccording to an article in Pediatrics, the official journal of the American Academy of Pediatrics (AAP), independent toilet use is a major milestone for your child, combining new physical capabilities with an understanding of social expectations, and their own motivation to become more autonomous. The article noted that toilet training is also one of the most difficult milestones for children and their parents, and that it can become highly emotional. Self-esteem can be fragile at this time, so it\'s important to toilet train gently, letting your child lead the way. Additionally, it\'s unwise to begin potty training unless your child is truly ready. Take this potty training readiness quiz featured in Parents before you begin.\nElizabeth Pantley, author of The No-Cry Potty Training Solution, explained in an excerpt on Child Development Info that most toddlers pee four to eight times per day. On top of that, toddlers have one or two bowel movements a day. But every toddler is an individual. Some will go more often than that, and others will last a couple days without having a bowel movement at all.\nIn terms of actually getting your toddler to the potty, Pantley suggested setting up a potty routine. Potty first thing in the morning, after eating, and before other activities, like riding in the car or going to sleep. Of course, you can adapt this routine to your lifestyle, and you still must be on the lookout for signs your toddler has to go ahead of schedule. If he or she looks squirmy, take them to the potty. But if you miss the signal, and there\'s a mess, it\'s no big deal. Practice makes perfect, after all. Don\'t let emotions get the better of you, even if your little girl or guy pees on an expensive piece of furniture.\nTry to get your toddler to the toilet frequently, but remember that it\'s OK if she needs a day off. According to Becoming the Parent You Want To Be by Laura Davis and Janis Keyser, it\'s common for children to go back and forth — somedays preferring diapers, and other days selecting to use the toilet. They recommended thinking of "accidents" as "opportunities."\nPantley also suggested visiting new restrooms when you\'re on the go. Frequent visits to toilets far and near may help habituate your child to independent toilet use. Keep in mind that not all children will want to use strange bathrooms, and don\'t force anything. Davis and Keyser stressed the importance of keeping your own emotions in check throughout the toilet training process.\nThe bottom line: when it comes to potty time, there\'s no magic number, but it\'s a good idea to take your toddler to the toilet often. Begin by following a schedule — morning pee, before nap time pee — and remember to look for signs that they\'re holding it. You can only take your child to the bathroom too much if it begins to feel stressful or punitive. If negative emotions attach themselves to toilet time, it\'s OK to take a break. It might take some time to achieve that no-more-diapers party, but that\'s fine. You\'ll just have that much longer to plan a good one.\nMay 27. 2021\nSEARCH CLOSE\nPregnancy\nSee All Trying Birth After\nRaising Kids\nSee All Baby Toddler Little Kid Big Kid\nYou\nSee All Sex & Relationships Wellness Style\nLife\nSee All Food Home Entertainment Politics Shopping\nHealth\nAbout Archive Terms Privacy Newsletter Archive Advertise Masthead Editorial Standards\n© 2021 Bustle Digital Group. All rights reserved.', 'docid': 'msmarco_v2.1_doc_51_766815931'}
```

Example from MS MARCO v2.1 Segment collection:
```python
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

## OUTPUT from participant
Output containing the following JSON information as <`rag_output_trec_rag_2024.jsonl`>. You can feel free to use any document/segmentation choice of yours, however, to make this collection reusable, we require the participant to map their custom chunked segments with segments available from MS MARCO V2.1 segment collection and provide us back the JSON output shown below:

```python
{
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
        "response_length": 1090, 
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

We will now build baselines for the tasks and finalize topics as the next step!

Our task information is at a draft stage, hence we encourage the community to provide us with constructive feedback regarding any task, or require us to further clarify any task.
Please feel free to reach out to us via Twitter/Discord!


*The TREC RAG Organizers Send Their Regards.*