# Entity-aware Transformers for Entity Search

[Link](https://arxiv.org/abs/2205.00820)

## Intro

Pretrained models learn rich contextual information about words from large-scale unstructured corpora.
It is good for NLP tasks and IR tasks.
These graphs capture info about entities otherwise found otherwise in knowledge graphs [35, 42].
Such that models can predict masked objects in sentences.
But they fail in complex reasoning over entities - bad at sparse world facts. [23, 35, 39].
Recent works enhance models with entity info from kg.
That gives a good performance [23, 34, 37, 43, 45, 50, 54].
But none of these examined the effect of entity enriched language models for answering entity oriented queries in IR.

This work explores the benefit of enriching bert retrieval models with entity info from kgs for entity retrieval rather then passage or documents.
It is shown that entity info improves document and entity retrieval [9, 15, 18, 47, 48] without language models such as bert.

The problem is there is limited training data and fine uning that leads to instabilities in model performance.
The dbpedia dataset v2 contains a little data for fine tuning.
The training data should be large, otherwise it causes forgetting.

- Tasks
  - Can an entity-enriched BERT-based retrieval model improve the performance of entity retrieval?
    - they propose enriched bert model, where factual entity info is injected to monobert from wiki2vec entity embeddings, that are transformed into word piece vector space
    - it is first trained on ms marco passage dataset and further fine tuned on dbpedia dataset
    - they also show that finetuning of the plane bert models (monoBert) on dbpedia is brittle and prone to degenerate performance
    - the same process is stable when using eneity enriched bert model
  - Which queries are helped by em-bert?
    - It helps queries that are anotated with at least one entity
    - plain and eneity enriched bert models pertform on par witch each other for queries without linked enetities
    - they find out that em-bert is most helpful when eneity mentions are broken into multiple word pieces by bert tokenizer
    - which means that directly injecting entity info into bert based models is particularly important for less popular eneitites
  - Why does it work and what does it learn during fine tuning?
    - learned eneity repre form a cluster
  - How does the model perform on other ranking taks?
    - passage ranking is good even without enriched model

## Related work

- graph embeddings
  - transE
  - Wikipedia2vec
- entity retrieval
  - 07 paper
  - 05 paper
  - ent-rank
    - entity neighbour text relations in learning to rank model
    - incorporates entity neigbor relations and performs competetively
  - beir benchmark  
    - retrieve bm25 candidates and then uses miniLM  cross encoder trained with knowledge distillation setup provided by [Improving Efficient Neural Ranking Models with Cross Architecture Knowledge Distillation]
- entity linking - the process of automatically linking entity mentions in text to the corresponding entries in a knowledge base
  - they use rel 
    - which detects mentiones using flair embeddings
    - it performs candidate selecetion based on wikipedia2vec embeddings and eneity disambiguation based on latent relations between entity mentions
- transformer based rankers
  - bert is fined for binary relevnace classification feeding it a sentece A and sentence B and using BERT classifiert token to predict relevance.
    - MonoBert is a point wise reranker in which the bert model is used as binary relevance classifier
    - the thing first used bm25 and then used monobert feeding it query and sentences to find the best relevant entities
- entity and transformers
  - enriching info about entities
  - ERNIE
    - finetuning with the combination of entities and text
  - KnowBert
    - adding knowledge attention and recontextualization componenent
    - this improves entity linking
  - e-bert
    - it does not need any additional training of the network
    - it only requires computation of one large transofmation matrix
    - this allows the method to be fine tuned transformer model

## Method

### Background

Kg embeddings provide vector repre of enetities by projecting entity properties and relations into a vector space.
Thse can be done based on purely tological data or combining text.
In this paper they use Wikipedia2Vec.
Following [37 e bert], they transform wikipedia2vec entity embeddings into bert word piece space and use them as input to the bert model.

- Wiki2Vec embeds a list of words and list of entities
  - the training is done with
    - predict context of words of a given words
    - predicting neighboring entities
    - predicting anchor text pf an entity to combine words and eneitites
  - they use lookup function to trnasform word pieces into native bert word piece

### EM-BERT

The model incorporates entity embeddings into a point wise document approach.
They combine e-bert with mono-bert and predicts retrieval score for a query document pair each represented by a sequnce of words and entities.
The model takes as input concatenation of query token and the document tokens where the tokens are either bert wordpiece tokens or entity token.

- entity enriched bert
  - it accepts its native word pieces
  - to incorporate enetity embeddings into bert, they need to align entity vectors with word piece vectors
    - following [37 e-bert]
    - linear transformation of entity vectors to bert like vectors
  - the aligned vectors are fed to the bert when an entity is mentioned in the input text
  - the entities are obtained with annotating text with entity

- retrieval
  - based on monobert
    - which is multi stage ranking method with bert 
    - first ranking based on bm25
    - the top k docs are passed to second ranker - here a bert based retrieval model
    - for every query-document pair is passed to bert to retreived
    - the bert classification vector is used as input to a signle layer neural network to obtain the relevance of document with the query
    - the model is trained :/

To sum it up.
First they learn the mapping matrix.
Then all queries and documents are annotated with an entity linker, and tagged quries and documents are tokenized and mapped to the corresponding vector presentations.
This input is fed into the em-bert model and then it is tuned on multiple collections.

## Evaluation

In the intro.