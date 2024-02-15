# Graph-Embedding Empowered Entity Retrieval

- [Link](https://arxiv.org/abs/2005.02843) (2020)

## Intro

There is growth of kbs and a rise of entity-oriented tasks.
Recently embeddings of words were used for entity retrieval.
However, a natural representation would not just represent words in conctext of their textual neighbourhood, but in context of the knoweldge graph instead.
They want to use graph embeddings instead of word embeddings, where the space not only encode textual context of an entity mention, but also context as difend through kg.
In wikipedia the embeddings would consider not only the page itself as context but also its anchor text.

They studies two stage approach where the second phase employs graph embeddings for reranking the results of state of the art entity ranking methods.

RQ1: Does adding graph embeddings improve entity retrieval methods?
RQ2: Which queries are helped the most?

They rerank the candidates using similarity between entities in the query (using of the shelf entity linked).

## Related work Embeddings

We have word2vec and glove.
There is a good method for expanding query with word embeddings, that expands query with locally learned words that are similar to the query.
There is a method that uses bm25 scores as labels to predict relevancee between query and documents.

There are graph embeddings to not encode only words in tet, but words in conctext of semi structured documents represented as graphs - e.g. distinguish between word in title or description.

Methods like deepwalk expect non labeled edges and can consider extensions of the word embedding approaches above.

There are other like TransE - where they learn representation of triples with names.

Wikipedia2Vec applies graph embeddings to Wikipedia, creating embeddings that jointly captures test and links.
The method embeds words and entities in the same vector space by using word context and graph context.
The word-word context is modeled using word2vec, entity-entity context considers neighbouring entities in the link graph and word-entity context takes the words in the context of the anchot that links to an entity.

### Related work Entity retrieval

Entity is object or concept tha can be distincly identified.
Methods for document retrieval wre used for entity retrieval.
Subsequently a fielded approach was used.
Such methods include FSDM, bm25f.

### Related work Entity linking

Linking entities mentioned in the quer to the kg enables the use of relationships encoded in the kg.
Previous work shown that it can boost efectiveness.
! In this research they use TagMe entity linker, since it is used to anotate short and poorly composed text like queries. 
! TagMe adds wikipedia hyperlinks to parts of text.

### Related work using embeddings for entity retrieval

Previously people used TransE, it showed a consistent improvements but small.
TransE is not a good choise if the graph has 1 to many, transitive or symetric relationships.
! In this research, they use graph embeddings but use Wikipedia2Vec.

## Embedding based retrieval 

### Graph embeddings

They train the entity embeddings on Wikipedia2Vec.
The Wikipedia KG is input, wikipedia2vec extends the skip-gram of word2vec and leanrs word and entity embeddings jointly.
The objective function is composed of three components:
1. infers optimal embeddings for words W in the corpus
2. considers link based measure estimated from kg, this measures relatedness between entities in the kb, based on similarity etween their incoming links
3. places similar entities and words near each other by considering the context of the andchor text

### Reranking

Training wikipedia2vec on wikipedia learns vector for each entity, but how to use them.
They first retrieve candidate set and then rerank the entities based on their similarity to the query entities.

For each query they obtain links to entities and their score - how much relevant are they for the score.
Then compute relevance for each entity in candidate set.

Then they interpolate the embeddings with the scores that retreived the dataset.

## Experimental setup

For evaluation they use dbpediva entity v2 set that contains queries and answers.
Wikipedia2Vec provides pre-trained embeddings.
These embeddings are not available for all entities in Wikipedia, e.g. 25% of entities in the eval. have no pretrained embeddings.
The reason is:
1. rare entities were excluded from the data
2. entity identifiers evolve over time
For training new graph embeddings they used new wikipedia dump.
They identify mismatch problem by identifying entities that have been renamed in the new dump.
Some were obtained using redirect api of wikipedia, others were found by matching wikipedia page ids.
For the missing ones they obtained them from nordlys package.
They changed setting of wikipedia2vec to include rare entities.

## Evaluations

The results show that the embeddings based scores do not perform well, but should be combined with other scores.
But it improves performance well.
BM25F have a better performance overall.
The result is that the graph embeddings do well.
The usage of tagme tool might be open web api to use.