# BERT-ER: Query-specific BERT Entity Representations for Entity Ranking

[Link](https://www.semanticscholar.org/paper/BERT-ER%3A-Query-specific-BERT-Entity-Representations-Chatterjee-Dietz/95786e847d7d73911f3718cf59408ad9a9d5beb8) (2022) should be better then E-BERT

## Abstract

In this work, they present bert entity representations which are query specific vector representations of entities obtained from text that describes how an entity is relevant for a query.
Using bert-er can achieve a performance boost over a bert embedding of the introductory paragraph from wikipedia.
Their approach also outperforms entity ranking systems using entity embeddings from wiki2vec, ernie and e-bert.
They also release the bert models and query specific entity embeddings fine-tuned for entity ranking task.

## Intro

Important aspect of entity oriented research pertains to the representation of entities.
Commonly a vector of the intro paragraph from an wikipedia article [35,36,58].
The problem with this is that it contains generic info which might usually not be important for the query.
They argue that the lead text was useful in less then 50% [16].
The embedding is static, meaning it is the same for every query.
Similarly this is for graph embeddings [5,33,51,56].
Recently ernie and e-bert were proposed to inject information from kg to bert.
These models too use static description from entity.

Why is it?
It is easy to compute and store.
There are good for query independent tasks - linking, typing, classification relation.

This might be bad for queries.
Static embeddings without any knowledge of the query may not be able to identify when two entities are similar in the context of the query.

Out hypothesis is that an entity embedding that incorporates query specific knowledge would be beneficial.
They use query specific textual description of an entity to encode the query relevant information about entities using bert.

- Task
  - given a query and entity - produce an embedding
  - they argue that bert have a poor performance.
  - but it is easy to use.
  - so they propose the bert-er which is also easy to use.
  - they explore query specific textual descriptions of entities for learning query specific entity embeddings using bert
    - aspect
      - top level section from wikipedia
      - they find the relevant sections and use the text as description
    - prf-passage   
      - most straightforward
      - pseudo relevance feedback and entity linking
      - they use the text of the highest ranked pseudo relevant candidate passage that mentions an entity as entity query specific textual description
    - entity support passage
      - is prf passage that mentions entity and explains why is it relevant

## Related work

### Knowledge enhanced bert 

They want bert model injected with knowledge.
- ERNIE
  - they add new layers to encode knowledge from entities into text from underlying layers
- KnowBert
  - a bert that models explicitly entity spands in the input text and uses entity linker trained jointly with the model to retrieve embeddings
- KEPLER
  - based on roberta that maps text and entities onto the smae space using same lm. and jointly optimizes knoedge embeddings nad the masked language modeling objectives

Ernie and KnowBert needs additional pre training, e-bert does not.
E-bert was shown to outperform bert, ernie and knowbert on multiple fields.

### Entity embeddings

- TransE 
  - problems with relations 
  - entities and relations are in the same space  
- TransH
  - representing each relation with two vectors (one norm and translation vector)
  - entities and relations are in the same space  
- TransR
  - separates entity and relation space
  - but for relation all entities share the same mapping matrix irrespective of their types or attributes
- TransD
  - unique mapping for every entity mapping
- TextEnt   
  - nn model leanrs distributed representations of entities and documents directly from knowledge base using intro paragraph from wikipedia article
- Wiki2vec
  - skipgram model to learn words and entities into one space
- GEEER
  - reranking with wiki2vec

### Entity ranking

- unstructured models
  - bm25
  - sfm
- fielded unstructured models
  - fsdm
  - bm25f
- learning to rank
  - [52]
    - features like the candidate entity is contained in the query
    - entities in queries and documents are connected in the graph
  - fielded document
    - [21]
  - ent-rank
    - combines info about an entity, entity neighbours and context using hypergraph
  - lts-asp
    - that entity aspects are useful for entity
    - a rich set of features from entity aspects
    - [9] aspects
- ranking via types
  - estimate type-based similarity between an entity and the set of target types provided with the query
  - [26] represents types by concatenating the desc. of entities that belong to that type
  - [1] query and entity types using prob. dist. and measure similarity between distributions

## Entity representation methods

Given a query and entity, they want to produce vector.
They use query-specific desc., text that states why an entity is relevant to a query.
Apparently it is easy to implement.
They obtain the query specific representations by fine-tuning bert for entity ranking task.


### Fine tuning bert

MonoBert and DuoBert for reranking for passage reranking.
They fine tune bert for entity ranking in two ways.
First they do point wise MonoBert style.
The pair wise DuoBert style.

The input to the bert is [cls]query[sep]desc[sep]
Somehow the in the output they take [cls] token embedding as the query specific embedding of entity e.

### Aspects descriptions

Based on aspects dataset.
Dont want to do this.

### PseudoRelevant descriptions

This is also based on the aspects.

### Entity support passage

Also dont want to do this.

... Skipping to Entity ranking

## Entity ranking

They use point and pair wise ranking methods to fine tune bert for the entity ranking task using the specific query-entity descriptions and obtain vector repre of an entity.

They learn some weight matrix to compute score.
Then then combine the ranking with the list wise ranking with other relevance features.

- Additional features
  - they obtain entity ranking by retrieving wikipedia pages from a search index
  - they also retrieve entities directly from an index containing the name and lead text of entities

## Experiment methodology

Again car dataset and dbpedia v2

## Evaluation

It is good for general question answering.
Otherwise from the tables it seems that the simpler keywords and list search are not that far behind.
The main idea is that the leading passage is not good for representing the query answering.
But in my case, there are no question aswring, just finding the right class.