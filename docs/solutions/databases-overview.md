# Databases

This file contains a brief selection of databases and their features that I deemed good for the tasks.

## Fulltext databases

### Elastic search

- i know it the most
- the elastic search in wikidata is using script score to compute relevance to the query based on the incoming links and sitelinks
- ranking
    - **rank features**
      -  to increase relevance based on fields in the docs, it enables using the top-k optimizations without iterating over all result set
    - **script score**
      -  does computation over all returned results in the query, computes the script on all matched documents
    - the scoring is **not normalized** for bm25, it uses a paper to generate rank features that are similar to the bm25 scoring
- allows filtering
- searching
  - text search
    - bm25 and **combined fields** for bm25f
    - the scoring of bm25 is not normalized and connot be done, only if you executed the query twice
  - **vector search**
    - uses hnsw graph
    -  in vector search a document cannot have multiple vectors
      -  but a field can be split into two vectors manually
    - filtering
      - elastic search mentions, that it filters **during the querying** of knn and it **does not do a post filtering**
    - it supports approximate and excat brute force knn
  - Semantic and hybrid search
    - One problems is that the ELSNER model is for paying users and in general cannot use sparse vectors.
    - As well as the reciprocal rank function.
    - combine knn with bm25 using rrf out of the box
    - semantic search using elsner sparse encoder
  - elastic can disable storing of the data and just do the indexing
  - it enables subfields on one: original text and keyword type
  - it enables to use language analyzers, tokenizers, and normalizers
  - enables rescoring - **Wikidata native boosting**

### Typesense

- more simple than elastic search but less verbose
- it should be faster
- ranking
  - does not allow user functions
  - just ordering 
- text search
  - does not include a specific algorithm just a series of notes
- vector search is enabled
  - hnws index, approximate match and exact match
  - does not allow multiple embeddings
  - allows hybrid as in elastic search
  - also allows ranking matches by embeddings
    - this could be done in the es aswell with script score
  - does not mentions how the filtering is done

### MeiliSearch

- ranking
  - allows custom rules for ordering but not functions as in elastic search but only as reordering
  - the score is always [0,1]
- text search
  - as in typesense, and based on algolia
- vector search
  - experimental features

### Solr

- feature wise it is not better than elastic search

### Opensearch

- based on elasticsearch fork
- the only benefit to elastic search is that it allows post query normalizations

## Vector databases

### Elastic search

- filtering during computatoin of the knn, pre filtering
- approximate and exact

### Waeviate

- pre filtering
- bad for hybrid query since it does not contains better matching
- hybrid search as before

### Qadrant

- Seems good for filtering.
- Simple api
- Nice documentation

### Vespa

- A badly organized documentation, tedious set up.
- But nice features on ranking given user functions.
