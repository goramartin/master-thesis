# Query Expansion Using Contextual Clue Sampling with Language Models


- [Link](https://arxiv.org/abs/2210.07093)

## Intro

One recent line uses llms to generate query related context for expansion.
They argue that expansions terms from these context should balance: diversity and relenvace.
To balance diversity is to sample multiple context from the language model, but this comes at the cost of relevance - because models hallucinate.

They propose combination of an effective filtering strategy and fusion of the retrieved documents based on the generation probability of each context.

It is better then some dense retrieval model DPR, and it reduces size of the index by 96%.

## Related methods

Still lexical matching because they are smaller.
Hybrid methods like splade.
In recent work GAR [Generation-augmented retrieval for open domain question answering] - removing query expansions reliance on an external corpus and instead used llm to generate context.

They argue there is a need for diversity and relevance.
Diversity there are multiple paths to answer, and simply relying on single context can be bad [schuze 2008]

## Method

They use filtering and fusion.
After retrieving top k from encoder contextual clues, they cluster them based on their lexical distance.
In each cluster, they keep only single context, with heighest generation probability.
The filtering step reduces potential factual errors and redundant close duplicates.
The query is then augmented with each filtered context.
They query the database separately.
The documents are then ranked according to the generation probaility from integral contextual clue in the augmented query.

They use seq2seq model - given question, generate the contextual clues.
Contextual clues are the sentences in a passage that contains the ground truth answer to the question.
The senteces are extracted from passage provided by the dataset or from matching passage used as a reference for the retriever.

- I am missing some information how they actually got the generation probabilities for filtering
  - they fine tune bart model for clue generation
  - given a question - they generate 100 outputs from bart using beam search with beam size 100.
  - they cluster the candidates using fuzzy string matching

## Baselines

BM25.
DPR implements retrieval by repsenting question and passages as dense vectors.
GAR proposes to expand query by ading relevant answers, the title of a passage and the sentence where the answer belongs.
It is mainly for the passage ranking.

## Comments

It works, but not sure about the fine tuning the bart model.
- papers that are similar and used a lot through out the paper
  - [Dense Passage Retrieval for Open-Domain Question Answering](https://arxiv.org/abs/2004.04906)
    - basically they learn dense vector embeddings and then retrieve
    - dpr naming
  - [Generation-Augmented Retrieval for Open-Domain Question Answering](https://aclanthology.org/2021.acl-long.316/)
  - [BART: Denoising Sequence-to-Sequence Pre-training for Natural Language Generation, Translation, and Comprehension](https://arxiv.org/abs/1910.13461)
