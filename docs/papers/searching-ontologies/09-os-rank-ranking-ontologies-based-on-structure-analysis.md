# OS-Rank - Ranking Ontology Based on Structure Analysis

[Link](https://ieeexplore.ieee.org/document/5362262)

## Intro

Previous attempts in ranking did not utilize structure information of the ontology.
Ontology can be regarded as a formal specification of a shared concept set of a certain domain - the structure and the semantic hierarchy can be seen as representing the rule and knowledge of this domain of interest.
They propose OS_RANK - how concepts are covered and detailed in the ontologies.
They propose also a measures similar to tf/idf.

## Ranking meethods

The query terms are mainly regarded as the classes defined in the ontology.
The importance of a class in an ontology should be determined by not only the frequency of the class label appearing in the ontology but the importance of struture and semantic relations of this class with other classes.

- Ranking class name
  - the input are user's query terms
  - they look for classes exactly matched or partially matched
  - the larger number of matches in the ontology, the better the ontology
- Ranking ontology structure
  - Is there a good representation of a concept in the ontology? -> How large is the coverage of the concept?
  - Simply the more sub/super classes that the classes matched with the query terms have, the more deiled the query terms are in the ontology.
- Ranking semantic structure
  - it ranks semantic associations
  - adjusted tf/idf - rank the number of semantic arcs and the importance of the semantic arcs at the same time (arcs are outgoing and incoming properties)
  - tf - the ontology is better if there is a lot of arcs between the matched classes in the ontology
  - idf - is for the specificity 
  - DatatypeProperty -> outgoing edge
- Ranking domain concept
  - when user submits concepts as query terms, there are potential semantic ambiguities and determining the domain is rather difficult
  - the wordnet is used for disambiguation and to find other domain concepts related with the query terms 
  - upon term insertion into the query -> user is promted which meaning he wishes
  - they can find other concepts that have semantic relations with the queyr terms
  - so they create sort of corpus and subsequently say that the more terms from the domain the ontology has the better it is