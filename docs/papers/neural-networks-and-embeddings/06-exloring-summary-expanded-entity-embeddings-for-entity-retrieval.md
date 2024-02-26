# Exploring Summary-Expanded Entity Embeddings for Entity Retrieval

[Link](https://ceur-ws.org/Vol-2482/paper7.pdf)

## Intro

Entity retrieval - return a ranked list of entities relevant to the user's query.
Entities meaning that is similar to the query.
Previously problem with semantic similarity between terms, text and sentences.
Then word embeddings came.
Word2Vec represents vocabylary terms by capturing coocurrence information between the terms, using likelihood approximation of terms appearance within a window context.
There was a substantial work for defining embeddings for entities but there is no clear baseline fo ranking entities with such compressed semantic representations.

When trying to reuse task specific entity embeddings for retrieval, results can be less than impressive (transE).
RDF2Vec was designed to data mining but underperform in retrieval baselines such as BM25 [29].
Fully deep models exists, but they do not have enough data.

They propose method that entity embedding is based on other entities crucial to its summary. 
They use entities that appear inside dbpedia abstract.
They use links in them, since htey were added by human.

They say it is better then query expansion or single word embeddings.

## Related work

- laveraging kb for er
  - previous works study the use of type info to improve retrival accuracy
  - entities in form or tuples (rdf)
  - they use fielded retrieval methods bm25f or fsdm
  - use of fields from fsdm paper
- no kb for er
  - finding locations in text
  - linked web pages and queries
- neural networds 
  - word2vec - skip-gram pr cbow
  - glove - matrix factorizations
  - used for academic search, disambiguation, question aswering or graph completion
  - rdf2vec is not effective for retrieval task


## General sheme of retrieval

Vocabulary mismatch is a problem - word embeddings were proposed to mitigate the problem.
They investiage the effect of word embeddings in entitry retrieval to solve mismatches.

They hypothesize that mapping the query to entity space and comparing with retreived entities will improve the retrieval results.

The entities here are represented as a short text.
They first create candidate set as well using some term based model. 
They use two methods:
- WordVec
  - each word in the query is made to a vector and average is made
  - that is the final vector
  - entities are also represented in the similar way
  - by averaging words in the abstract
  - they use GloVe pretrained model
- EntityVec
  - embedding vector for entities is learned based on the skip-gram model in genshim (word2vec)
  - in learning they replace hyperlinks in the abstracts with entity names and type
  - queries are represented by average of embedding vectors of entities in the query
  - entities are anotated using TagMe detection tool
  - (isnt this based what if the entity is not inside?)
- final embedding is average over embedding vectors of referred entities appeared in the abstract of the targed entity
- final score is interpolation between baseline nad the models
- all in all, they always do aeeraging on the vectors

In this paper they are against query expansions.
The baseline for query expansion is RM3 apparently state of the art.
Since this approach in embeddings does exactly this.

## Evaluation

Both methods are better than baselines - some term based model and query expansion with pseudo relevance feedback

They note that both methods imporove significantly verbose queries (longer than 4 terms).
The more words give better disambiguation.
For WordVec vector the embedding does not improve significantly with short queries.
This can be since short queries can be more specific so the embedding does not play such a large part.
The entity including in the abstract is somewhat beneficial.

They note taht combining the two models can be beneficial.
Which means the two methods are complementary and capturing different aspects.

Also interesting aspects are that the query expansion with the models is beneficial and means that the models are orthogonal to the query expansion.


