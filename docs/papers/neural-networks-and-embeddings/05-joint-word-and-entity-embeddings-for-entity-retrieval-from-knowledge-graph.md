# Joint Word and Entity Embeddings for Entity Retrieval from a Knowledge Graph

[Link](https://link.springer.com/chapter/10.1007/978-3-030-45439-5_10)

### Intro

It is mainly used for nlp questions.

Previously models for ad-hoc entity retrieval based on direct term matching which suffer from mismatch between vocabularies in entities and in queries.
There were some successful applications with word embeddings and graph embeddings to adress word mismatch and graph noisiness.
The joint embeddings have not been utilized yet.

Entity retrieval document based methods.
Those take only adjacent components of a knowledge graph when constructing a document for entity.
Which is not taking into account the local structure of knowledge graph that are separated more than one edge in graph.
Entities are points in high dimensional space equal to vocabulary size.
There is a gap between queries and documents.
The mismatch was somewhat solved by language model embeddings.

To address noisines of graphs methos like rescal, transE and NTN were created.
They represetn entity and relations as vectors in the same embedding.
Good for knowledge graph link prediction.
Methods like DeepWalk, Line and Node2Vec do not consider words.

They propose a method to create embedding based on entites and words in the same space.
It samples random walks and is hybrid between word and network embeddings.
It utilized ocntextual co-ocurrences as traning data, as in word embeddings, it treats words and entities as different objects.
It takes into account local graph structure but differentiates between structural component

### Related work

Previously only knowledge graph structure.
Then a fielded entity representation from a graph then treat it as a document.
Entity similarity from embeddings were used in reraking of term based models using learning to rank.

Word embeddings good.

Network embeddings good.
The methods adopt from NLP to model sequences obtained using random waslk on a given network.
Such as deepwalk, line, node2vec and struct2vec.

Knowledge graph embeddings created vectors for entities and properties.
TransE is good.
Member and Glove for learning spaces of word and entity embeddings in which words and entities are separated by hyperplane.
There are tries to combine transE and word2vec in one loss function.
None of the methods were proposed for entity search.

### Method to learn embeddings

The primary goal of the proposed method is to learn joint word and entity embeddings that are effective for entity retrieval from a knowledge graph.
Idea is related to the idea that graph consists of key structural components.
It is somewhat related to structural components used in entity documents.

The method uses neural architecture that utilizes as inpput a set of sequencs of word tokens and entity uris produced as:
1. perform random walks over a kg to generate sequences consisting of structural components of a graph (eneitties, predicates, attributes and categories) of length t.
2. rnadomly with probability r replace uris in sequnces with their respective surface forms.

The objective during training is to predict a surrounding context given an element.
Given a node in the walk, it minimizes the embedding of context elements.

### Training objective

To obtain embeddings for words and entities and optionally cathegories and predicates.
A model is with negative skip-gram based model is used.
We have a set of random walks, the model maximizes the probability of observing elements in the walk from the context of current element in the walk.
The combine they use concatenation of in and out embeddings for words and out and in embeddings for entities.
Final vectors are of double size.

### Embedding based entity search

For a given Q, they calculate embeddings for each word in a query and compute weighted sum of embeddings of query words.
Where they use unigram probability of the query term in the corpus knowledge grapg literals.
For similarity they use cosine similarity.
This can be used for all entities or reranking scenario.

Not sure what the entity is here.
We write free text and compute word embeddings for the query and then do what?

### Evaluation

The used dbpedia english set and did a dataset construction.
For the lenght of walks they find that 10 is the best.
Also they say that all the components used are beneficial for the construction.
Their approach is better on its own.
But works better with reranking during complex question aswering.
Overall the results are not that different from their baselines.