# 2. Meeting 

This meeting I would like to talk about:
1. Brief overview of what I did.
2. pipeline
3. picking solutions
4. subclassing with properties

## Brief overview of what I did

- From previous meeting:
  - [x] 1. Thing about general pipeline and solution selection.
  - [ ] 2. I wanted to check the learning embeddings and knowledge enhanced lm.
  - [x] 3. Create a summary on my comments from searching ontologies and class importance.
  - [x] 4. Think about solutions based on the property selection filtering.
  - [x] 5. Check databases and create an overview.

## Pipeline

![Picture](02-picture-pipeline.drawio.png)

- Query expansion
  - using LLM
- Candidate Retrieval
  - Connection to a search engine: text search engine, vector search engine
- Reranking
  - Rerank candidates based on conditions
  - Can be in two steps
    - first phase reranking 
      - e.g. rerank all the candidates and pick top 30 
    - second phase reranking
      - again rerank the top 30 from previous phase with different conditions and present to the user

## Picking solutions

- Overview from previous meeting
  1. Full text search
     - load classes/properties with hand-picked representative information into a full text search engine and query   
  2. Vector search
     - lexicalize classes/properties and provide ANN search based on the query
     - choose a good embedding model
  3. Reranking the solutions
     - using similarity to embeddings
     - wikidata native criteria
     - subclassing
     - RAG
     - Entity linking
     - ? others

- Generally too many things.
  - I would like to exclude:
    - Entity linking, since I can make the front end in a way, that would make this solution not important
    - Choosing the right LLM and use the running model Mistral on our servers.
    - Probably training my own embeddings (But I still did not revisit the triple bert and knowledge enhanced models)


- I would like to focus on:
  - **Query expasion**
    -  using LLM
  - **Candidate Retrieval**
    - using full text search (ElasticSearch, Typesense)
    - using vector search (Qadrant, Waeviate Chroma)
  - **Reranking**
    - subclassing with properties
    - wikidata native search
      - linear combination of number of incoming links + number of sitelinks
    - using RAG with Mistral LLM

## Subclassing problem with properties

- A user wants to find a class with given properties.
  - User input:
    - class text input - name, description
    - properties text list input - name, description
  - Process
    1. find the best matched for the properties input list
    2. filter or rerank the results from class search
  - **pre/during-candidate selection** vs **post-candidate selection**
    - pre/during-candidate selection
      - where clause in sql
      - in the database use filter based on the properties
      - possibly time consuming
      - with the database it is difficult/impossible to give scores based on the containing properties
    - post-candidate
      - on the candidate list do filtering and reranking
      - faster but results might not be that good

