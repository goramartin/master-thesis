# An Integrated Ontology Ranking Method for Enhancing Knowledge Reuse

[Link](https://www.researchgate.net/publication/289725459_An_Integrated_Ontology_Ranking_Method_for_Enhancing_Knowledge_Reuse)

## Intro

This paper proposes integrated ranking based on the "content-based" and "ontology-rank" approaches.
They argue that with keyword matching it is impossible to find semantic meaning in the ontologies -> we need similarity matching.
The purpose of this paper is to propose a framework for the ranking.

- Revision of the approaches
  - content based
    - ranking is done based on the number of matching concept labels in ontologies with labels extracted from WordNet (corpus like)
  - ontology rank
    - difficult to be used in publicly available ontologies

## Combination

The input of the framework are the user's input terms.
The terms are used for querying Swoogle.
Then it downloads the ontologies and begins to rank them.
First the ranking is done based on the content based ranking, subsequently the result is given to the OR ranking (Relation match, taxonomy match, density match, class match).

- Content based 
  - the search term expansion is done using WordNet.
  - the keywords are expanded and given to the Swoogle for searching
  - the article is misleading in whether the expansion is done before puting into the Swoogle or after the results are gathered from Swoogle
    - it seems that it is done in both situations
  - the rest is the same
- OR
  - using the reduced model - Class match measure, taxonomy measure, relation match measure and density measure
  - CMM
    - coverage of ontology for a user supplied search term
    - it checks for classes in each ontology that having matching (exact match or partial match) labels to the search term
  - Taxo
    - semantic similarity of a taxonomy relation in a IS-A relation
  - RMM
    - as in OR
  - Density measure
  - Semantic similarity measure
    - checks the proximity of the concept of interest present in the ontology structure
    - it is calculated by counting the number of links that connects a pair of concepts
