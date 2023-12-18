# Ranking Ontologies with AKTiveRank

[Link](https://link.springer.com/chapter/10.1007/11926078_1)


A prototype system for ranking ontologies based on a number of structural metrics.
AKTiveRank is an experimental system for ranking ontologies based on a number of measures that assess the ontology in terms of how well it represents the concepts of interest.

> Note: This paper is an improved one. In this one they use improved measurements. E.g. They used previously Centrality measure - the closer to the middle level of hiearchy the better - they found out that the CEM corresponds to the density measures.

### Class match measure

Is meant to evaluate the coveage of an ontology for the given search terms.
They match the search terms with labels of  classes in ontology. The more matches the better. The exact matches are regarded as better then partial matches. It also considers the total number of partial matches, so more matches meaning more representation in the concept and thus the ontology should score higher score. But in general the partial matches can cause problems "gene" vs "generator", so the number of partial matches is limited only to the CMM.

### Density measure

One would expect to find a certain degree of detail in the knowledge graph regarding the concept - rich conceptual neighbourhood. This regards -> the number of subclasses, the number of properties associated and number of siblings. It is approximation of information content of classes.

In this paper they limit the density to the number of direct relations, subclasses, superclasses and siblings. They dropped the number of instances since it might skew the results unfairly towards populated ontologies which may not necessarily reflect the quality of the schema itself.

### Semantic similarity measure

Ontologies are semantic graphs of concepts, relations and hence similarity measures can e applied to explore these graphs. Previously: WordNet to resolve ambiguities. Another one is shortest path measure, the more relationships objects have in common, the closer they will be in the ontology. The SSM calculates how close are the concepts of interest laid out in the ontology structure. If concepts are far, then it is unlikely they will be represented in a compact manner. Basically it wants to compute shortest path between all concepts.

### Betweenness measure

The number of shortest paths that pass through each node in the graph. Nodes that occur on many shortest path between other nodes have higher betweenness value. The class is graphically central to that ontology. The classes that are move central will receive hiher BEM.


Other links:
- [framework for ontology evaluation](https://www.researchgate.net/publication/221565315_A_theoretical_framework_for_ontology_evaluation_and_validation)