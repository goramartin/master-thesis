# 4. meeting

This meeting I would like to talk about:
1. Brief overview of what I did.    
2. Filtering with subclassing
3. Topic modeling
4. Choosing embedding models
5. Language for the application

## Brief overview of what I did

- From previous meeting:
  - [ ] 1. Think about solutions based on the property selection filtering. (Ongoing)
  - [x] 3. Check which models would be good

## Filtering with subclassing

- What are the memory limits?

- Index all properties for each class
  - query = selected properties by the user
  - memory hungry
  - but simplest
- Index parents only
  - query = parents containing the properties
  - not that memory hungry
    - with reductions

## Topic modeling

- Additional filter to the subclassing
- How to further reduce the search space (vector search and full text search):
- Split the classes into cathegories
  - but to what cathegories?
  - methods that deduce the topics
    - wikidata cathegories
      - probably a lot of missing
      - sometimes it seems like 1 to 1
    - manually create the topics
      -  use similarity to the entity and topic
      -  ask llm to choose the topics
    - unsupervised learning
      - Topic2Vec, BERTopic
      - can generate a lot of topic
      - needs additional model to run
      - depends on the words
      - uncontrolled
      - mostly good for longer texts
- How to apply them:
  - the user chooses
  - or someone chooses based on the query

## Choosing embedding models

- symetrics vs assymetrics
- MTEB:
  - mixbread ai
  - sentence transformers
- usually low in side
  - model size 1.34 GB

## Language fo the application

- Thread parallelism
- Query expansion in the node backend node or search backend node
- Probably some data in the search node for reranking