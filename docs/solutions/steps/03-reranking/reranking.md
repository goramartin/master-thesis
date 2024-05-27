# Reranking

For theory visit papers.

## Reranking using the number of properties

- Assuming the user inputed some properties
- Retrieve initial results with the candidate selection either with or without a filter
- then assign higher score to the classes that contain properties
  - the most to the one containing all
  - then less for others
  - there would be no importance in the order of it, just the number
    - one could assume that the user would have written them in order
    - but that is not always a true

- dont thing this is a good thing, since i would like to have it as a filter
- but might be neccessary if it is way to slow

## Wikidata native search reranking

- number of incoming links to an entity and the number of sitelinks to the entity
- but i am not sure it is really true
- they use elasic search
  - either function score to change the scores
  - or do a sum to the score of the bm25 (rank features)
- it showed that the wikidata native search is much more complicated
- it so i have decided that i would do the incoming links and the number of external mappings

## Reranking with the similarity to the query on vector repre

- the idea is to use the reranking based on the similarity to the query
- for full text search:
  - easy
- for vector search:
  - we already have this, so then do what?
  - possibly just exlude it
- Not good based on Qdrant since it is not linearly combinables

## Reranking using cross encoder

- the idea is to get some cross encoder as the last step of the pipeline

## Fusion for hybrid search

- Based on paper convex combination is a good thing
- eighter 0.5 and 0.5 or give more to the dense things
- additional step could be the crossencoder
- it makes sense to first do the fusion and then the reranking on the documents (since we are adding linear combination), the cross encoder before fusion does not make sense since it would be fusion of very little elements

## Features for classes

- number of instances - satu with pivot of 100
- number of external ontology mappings - satu with pivot of 2
 
- based on experiments
- we want to boost classes that enable better modeling
- two factors mentioned above
- incoming links are highly collerated with the number of instances

- we can sum up the scores to 0.5, 0.5
- and to sum it up to the search score with 0.6 and 0.4

## For properties

- usage count - satu with 1000
- number of external ontology mapping satu with 2



