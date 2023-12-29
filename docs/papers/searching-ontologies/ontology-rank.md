# OntologyRank

[Link](https://www.sciencedirect.com/science/article/pii/S0957417410011310)

They provide a model for ontology selection and ranking.
It enables semantic matching of taxonomy or relational linkage between concepts.
It identifies what measures should be used to tank ontologies in the given context.
They adapt semantic similarity theory.

It proposes a framework - ontology rank.
The query input is key-word based - concepts as keys but it adds hierarchical and non hierarchical relations.
Previously, methods focused on lexical level keyword matching.
Problems with this: difficult to find similar words, it cannot disambiguate meanings of polysemy (no context), no relation mathing.
To solve these problems three methods are proposed:
    - using synonyms of given terms for similar words
    - polysemy preprocessing - query interface to add context
    - no solution for relation matching - this is the topic of this paper.

### Semantic matching based on semantic similarity

- semantic similarity is integration of concept similarity, relational similarity and taxonomic relational similarity.

- concept similarity 
  - comparing search terms with concepts in the ontology
  - semantic similarity considers exact match, partial match and synonym match
  - they compute similarity of query in the ontology
- relation matching
  - how relation in the ontology matches the relation between search terms
  - based on four factos:
    - concept match
      -  deals with the correspondence between concepts and search terms
      -  F(o, T) checks whether domain and range concep are matched exactly or partially with search terms.
      -  this can be done by concept matching
    - relation label match
      - degree of corespondence bwetween relation labels Rs and Rc
      - Rs relation bewtween search terms, and Rc refers to relation between concepts matched by search terms
    - distance between concepts
      - distance between domain concept and range concept of a relation
      - minimum path length between two concepts
      - edge counting path length between domain concept and range concept 
      - exact match if domain and ragne are connected and indirect otherwise
    - neighbour match
      - it check whether the domain and range concepts of a search relation can be connected with the help of their neighbour nodes
      - inverse proportion to the number of concepts in the neighborhood of concept
  - RMM calculates the degree of semantic similarity of a relation Rs between search terms in an ontology o. A lot of formular - refer to the paper page (5)
- taxonomy matching
  - a metric to measure taxonomix relation
  - special type of relation matching
    - is a, super-sub, part of, equivalent...
  - but we regard only is a hierarchy
  - search for concepts matched by search terms and is a relation batched by is a relatoion between search terms
  - TAXO - taxonomy match measure
    - looks for two classes matched by the search terms and that also have a is a relation ship

### Ranking

- selection:
  - standarts:
    - how relenvat are searched keywords - semantic similarity
    - are the searched keywords main concepts - how many topics are matched with search terms and how precisely search terms are matched with topics in an ontology - topic coverage
    - how rich are the searched keywords defined in an ontology - density - richness

(the last two are from the aktive rank team but older paper)

The introduce linear combination model to comine chosen selection measures.
Based on context, choose the selection methods.