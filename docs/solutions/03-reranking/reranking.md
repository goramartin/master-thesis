# Reranking

## Reranking using the number of properties

- Assuming the user inputed some properties
- Retrieve initial results with the candidate selection either with or without a filter
- then assign higher score to the classes that contain properties
  - the most to the one containing all
  - then less for others
  - there would be no importance in the order of it, just the number
    - one could assume that the user would have written them in order
    - but that is not always a true

## Wikidata native search reranking

- number of incoming links to an entity and the number of sitelinks to the entity
- but i am not sure it is really true
- they use elasic search
  - either function score to change the scores
  - or do a sum to the score of the bm25 (rank features)

## Reranking with the similarity to the query on vector repre

- the idea is to use the reranking based on the similarity to the query
- for full text search:
  - easy
- for vector search:
  - we already have this, so then do what?
  - possibly just exlude it

## Reranking using cross encoder

- the idea is to get some oncoder 