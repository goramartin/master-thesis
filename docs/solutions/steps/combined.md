# Steps combinations

I was thinking what to implement eventually beacuse there are so many things.
And it needs to be user friendly because they will be conducting the searching and evaluation.

- We sort of gave up on the expansion at this point
  - Why?
    - Because I could not get some goot results.
    - There would be the need to run on the large language model.

Thinking about the databases Elastic and Qdrant


- Candidate selestion with filtering
  - Filtering 
    - Based on properties.
    - Either can be contains at least one, or must contain all.
    - This means the database has to have the ability to combine the filters.
    - Elastic - using terms query
    - Qdrant - using match any (in operator)
  - Candidate selection using the engines
    - Elastic search
      - Combined fields, Bm25 for text search
      - Enables restoring - wikidata native search
      - can use vector search but not the rrf and elsner model
      - slow index time
    - Qdrant
      - vector search with filtering
      - sparse vector search using the splade model
    - The problem is that Elastic cannot do sparse vectors except elsner models
      - and we need additional service just for the embeddings
      - both for elastic or client into the
    - Also there can be combinations
      - [combinatoin](https://qdrant.tech/documentation/tutorials/hybrid-search-fastembed/)
  - Reranking
    - Native Wikidata search
    - Cross encoder
    - Combinations
      - Reciprocal rank fusion
      - Relative score fusion
      - Distribute score fusion