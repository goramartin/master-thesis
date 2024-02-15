# Ontology Evaluation and Ranking using OntoQA

[Link](https://ieeexplore.ieee.org/document/4338348)


### Intro

A paper that presents a tool OntoQA that evaluates ontologies related to a certain set of ters and then ranks them. 
The tool enables users to tune the search results with selecting preference on a given set of ranking features.
It also evaluates ontologies with their instances (populated ontologies).
This paper is a novel approach based on their previous metrics - but this one should be better.

### Architecture based on components

1. Ontology
  - calculate metric values
2. Ontology and keywords
  - calculate metric values
  - use WordNet to expand keywords to include any related keywords that might exists in the ontology
  - use metric values to obtain numeric values that evaluates overall contents of the ontology and its relevance to keywords
3. Keywords
  - use swoogle to find rdf based on keywords
  - evaluate them as given in 2.
  - display ranking

### Terminology

- ontology schema 
  - a set of classes, relationshiops, inheritance function, class attribures
- knowledge base
  - a set of instances, instance function (gets instances of a class), relationship instantiation function (rel between two instances)

### Metrics

The evaluation is done in two dimensions -> instance level and schema level.
Schema level evaluates the design of an ontology.
Instance level evaluates placement of instance data.

- Schema metrics (I will not include the formulas)
  - Relationship diversity
    - looks at diversity of existing relationships
    - some ontologies have only inheritance relationships, while others may have much more diverse relationships
    - the tool gives a user option to select its preference
    - simply put it looks at the number of inheritance rels. vs non-inheritance rels.
  - Schema deepness
    - shallow vs deep ontology with regard to the number of inheritance levels
    - shallow have a low number of inheritance levels but each class can have a lot of subclasses
    - deep is the opossite
    - it is a ratio of the average number of subclasses per class

- Instance metrics
  - Overall KB metrics - a overall view how instances are represented
    - class utilization
      - how classes in the schema are being used in the KB
      - ratio of the number of populated classes and the total number of classes
    - cohesion
      - the number of connected components in the kb
      - not important for me
    - class instance distribution
      - how instances are spread across the classes of the schema
      - standard deviation in the number of instances per class
  - Class specific metrics - how each class in the ontology is being utilized
    - class connectivity
      - centrality of a class
      - how focal some classes are in the KB
      - we want classes that are central part of the ontology
      - total number of relationships instances of the class have with instances of other class
    - class importance
      - which areas of the schema are in focus (similar to conectivity)
      - it does not consider the real world semantics, where some classes naturally have more instances than others, class importance can still be used with connectivity measure
      - it is the number of instances that belong to the inheritance subtree rooted at the class compared to the total number of class instances
    - relationship utilization
      - how rels in the schema are being used in the instance level
      - it is the number of relationships that are being used by instances *I* that belong to a class *C*, compared to the number of rels. defined for *C*
  - Relationship specific metrics - how each rel. is being used in the schema
    - relationship importance
      - which relation ships are in focus
      - it is the number of instances of the relationship compaed to the total number of property instances in KB

### Score calculation

1. extend input keywords with WordNet
2. determine the classes and rels. whose names contain any extended term
3. compute the metrics and aggregate