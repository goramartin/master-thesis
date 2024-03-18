# Solution ideas

- why do we do it?
  - wikidata has a complex search but it is not possible to use programatically due to cors
  - also it has the wdsearchentities but it is too primitive
  - searching directly in the wikidata is not a good idea since we do not update the data in real time, so class information might be changed, also working with classes can be harsh in the wikidata landscape
  - so we produce our own search

## 1. Probabilistic Model BM25-Fielded (Sparse retrieval)

- classical search methods based on document retrieval, convert the node and property into a document and search for it
- probabilistic bm25f based on tf-idf
- used as a default amongst papers and general use in enterprise/research enviroments

- Store classes in Elastic Search and retrieve using BM25F implemnted by default in Elastic Search
  - the stored information is similar from GALAGO search system, and mentioned multiple times in papers
  - information to store:
    - base information
      - label
      - aliases
      - subclass info
      - most popular properties (probably cannot fit all of them)
    - additional information
      - description
        - this is tricky since it does sway the search results a little
      - has parts/part of
      - category
        - the cathogery usually contains the name of the class, which might not be the best thing here
      - has characteristics
      - different from  
        - difficult to provide context based solely on names of the entity here
      - has cause 
      - studied in
  - use term boosting on exact match and analyzers for languages
  - use wikidata api to search entities for better priority?

- Can be used as a first phase of retrieval, e.g. the first 1000 results
  - then combined with dense retrieval or rag
  - the query can be expanded using llms

### With reranking

- popularity is reappearing everywhere
  - number of instances
  - number of queries to wikidata
  - number of properties
  - number of site links
  - number of translations
- with reference to property input
  - find also properties from different text input
- centrality

## 2. Only embeddings

- Lexicalize entities and convert them into embeddings using some public pretrained language model
  - Lexicalization based on the [1]
  - could be multiple vectors
    - one with name and descirption plus base info
    - one with the additional data
- Use vector database for storing the embeddings
- Convert user input into the vector and query the database.
- it might be a slow solution

- What embeddings?
  - language models are deemed the best, lexicalization is the key part
  - knowledge graph embeddings
    - transE, complEx, and many more
    - bad for similarity but good for link prediction (their main use case)
    - rdf2vec worse than bm25
  - graph embeddings
    - deepWalk, node2vec, ...
    - based on networks
    - does not take node info into an account
    - there were tries - joint learning, but based on word2vec
    - there is graphSage - which takes into account info on the nodes, but no idea how to input the query into the space
  - embedding vectors are not that easy to combine into one to gain better performance
  - Knowledge enhanced language models
    - solutions on the wikipedia dependent, probably hard to reimplement to wikidata
    - needs pretraining the language model and needs finetuning and a lot of data
    - need more time to revise the solutions

- triple bert for learning better embeddings
  - can generate its data
- possibly bga and other models 

## 3. BM25F with reranking using embeddings

- To mitigate slow retrieval with 4M classes
- Use BM25 as in [1] and on the returned results use reranking by similarity to the query as in [2]

## 4. B25F with reranking using extracted entities from the query and embeddings

- entity linking might be superfluous if we make multiple text boxes

- Multiple papers used a solution which required entity linking from the query (TagMe, REL)
- They first used BM25F
- Then used entity linking on the query
- Extracted embeddings of the extracted entities
- Computed score based on the similarity with the entities and the BM25F score (60/40)

- More on entity linking in the papers folder `entity-linking`.
    - mostly based on sentences, not sure if its capable of finding keywords
    - missing data, very old data, missing code or instructions
    - does not work with aliases
    - generally linking to wikidata is not very explored
    - libs:
      - zshot
      - refined
      - falcon 2
    - maybe using llm prompts - not sure if it is capable of

## 5. All solutions with the query rewriting using LLM or Pseudo Relevance feedback

- Since expansion with LLM is bettern than Pseudo Relevance Feedback on sparse and dense retrievals
- Prompoting the LLM for
  - expanding the query with terms (similar to the given ones) 
  - or turn it into the sentence matching the stored/lexicalized information - might need more context
  - query2doc, query expansion, step back prompoting, rrr
- Rather dependent on the information provided with the query - might need some context

## 6. RAG with LLM

- The idea is to retrieve some portion of results using previous methods, and then use prompts on LLM to ask for the best results
- Can be as the last step in the pipeline 
  - expand the query with the terms
  - query using bm25f
  - reranking it using dense methods
  - top 20-30 rerank using LLM prompts
- Or different combinations
  - using only dense embeddings as in ontology alignment OLaLa paper

## General input

- text
- properties text
- ? cathegories

## What did not get in?

Keyword search over Knowledge Graph


