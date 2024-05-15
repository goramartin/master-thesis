# Entity Embeddings for Entity Ranking: A Replicability Study

[Link](https://link.springer.com/chapter/10.1007/978-3-031-28241-6_8) (2023)

## Intro

They study entity ranking since users seek entities in response to their queries.
Queries can be question like or seeking list.
Given a query, the entity ranking task is to return a list of entities ordered by the relevance of each entity to the query.

Previous works regard hand-crafted features withing L2R or use information about entities in a knowledge graph such as types and relations.
These systems, however, considers only lexical matching between queries and entity information and disregrad any semnatic structural information of entities.
To overcome this, reranking methods like TrasnE and Wiki2Vec have been proposed (like the paper 07 and 04 papers i read before).
Grapb embeddings capture the structural and semnatic information of entities in the context of the knowledge graph.

Additionally, Knowledge enhanced BERT models such as ERNIE and E-Bert were proposed.
The models augment the model bert with eneity information throught knowledge graph embeddings such as TransE and Wiki2Vec.
These embeddings are a fusion of entity information from KG abd rich text embeddings from bert.

In this paper they reproduce and replicate work from paper 08 i read before.
Since it is the first in a few papers to study utilization of kb embeddings in ER tasks.
Thy also incorporate learning to rank methods.
They also study the effect of neural fine tuning of the embeddings for ranking tasks.

## Related work

### KG embeddings

TransE, and it is bad for 1 to N or N to N relationships.
TransH and TransR were proposed.
Subsequently, Wiki2Vec was proposed to learn entity nad word embeddings using text and structural information from wikipedia.

### Knowledge-enhanced BERT models

The models enhance embeddings with the TrasnE or Wiki2Vec embeddings.
ERNIE uses TransE in pretraining.
While E-Bert adapts embeddings of Wiki2Vec withou any pretraining.
KEPLER utilizes entity descriptions corresponding to the entities in relation triples and optimized representations.
KELM inject knowledge in the bert via multi-relational subgraphs from knowledge graph and text.

### Retrieval with pseudo relevance feedback

Retrieval uses unstructured text of pseudo relevance feedback documents.
Entities and text features such as coocurrence and entiones can be combined thorught learning to rank approach.
Furthermore, kg links and entity coocurence from the feedback runs can be integrated.

### Retrieval with KG embeddings

Papers i read 04 and 07.

### Fielded models

bm25f and fsdm

## Approach

### Entity embeddings

- Wiki2Vec
    - shared embedding space for words and entities from wikipedia
    - it learns words with word2vec skipgram model
    - the similarities between entities is traned to coincide with wikipedia's link graph
- Ernie
  - injects transE entity embeddings in bert
  - it aligns entity embeddings of transE with bert embeddings of the first wordpiece token of the corresponding entity mention to generate encoded embeddings in a common space
- E-BERT
  - infuses wikipedia knowledge to contextualized bert wordpiece embeddings
  - aligns wiki2vec embeddings with bert word embeddings
  - e-bert uses word embeddings of wiki2vec to learn the weight matrix throught linear transformation of wiki2vec word em. to bert-like em.

### Finetuning neural networks

The original paper determines the reranking of candidates set though interpolation of embedding scores and candidate relevance score from the first stage, here they fine tune the approach.

For query, they find entities in the query, and average their embeddings to obtain a single eneity embedding of query.

They train bilinear projection with E^(T)_Q * W * E_C to capture correlations across different entries.
This is followed by a linear layer to predict the rank score.
The model is trained with a point wise loss and a pairwide loss using the test collection.

## Experimental setup

The setup is the same as in the paper 07.
To learn the interpolation they train l2r with rankLib as used in the original paper.

### Replicability and fine-tuning

They use TREC car dataset that emphasizes on entity types.
They use tag me again.

- Baseline - they use bm25f for dbpedia dataset and ent-rank for the trec car dataset.
- Embeddings - they use wiki2vec, ernie and e-bertI
- Interpolation - they change the l2r framwork to learn linear interpolation, they use rank-lips library using 5 random restarts.
- Fine-tuning - they use the same embeddings and they cannot train it on e-bert since they have no memory

## Results

They managed to replicate the results.
And found that those embeddings are beneficial.
In general, the scores with baseline + graph embeddings are not that great, the finetuned models are better.
The problem was they could not fine-tune the e-bert.
Overall, the wiki2vec was very successful with the baselines.
