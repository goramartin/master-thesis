# DWRank - Learning Concept Ranking for Ontology Search



[Link](https://www.semantic-web-journal.net/system/files/swj883.pdf)

it might have a previous paper - [Relationship-Based Top-K Concept Retrieval for Ontology Search](https://link.springer.com/chapter/10.1007/978-3-319-13704-9_37?fromPaywallRec=true)

## Intro

A two-staged bi-directional graph walk ranking algorithm for concepts in ontologies.
It characterises two features of a concept in an ontology to determine its rank in a corpus. 
The centrality of the concept to the ontology within which it is defined (HubScore) and the authoritativeness of the ontology in which it is defined (AuthorityScore).
They argue that most of the recent searchers use popularity score or use some sort of page rank algorithm which penalizes new but well designed ontologies.
Again, they propose a framework for retrieval of ontologies based on how well it represents a given search term.

Ranking in two steps:
1. offline learning and index construction
   - computing centrality of concepts
   - authority of a concept - it depends on the number of relationships between ontologies and the weight of these relationships based on authority of the source ontology - simply reused ontologies are better
   -  Ranking model is learnt from the  features using LamdaMart (L2R)
2. online query processing and evaluation againts a human

## Preliminaries

Ontology is a directed graph (V,E,L), where L(v) label function for a vertex, ontology or relationship.
We have explicit and implicit relationships between vertices.
Intra-ontology relationships and inter-ontology relationships.
Forward-link concepts and back-link concepts.

## Framework

In the first phase we have two indices - ConHubIdx and OntAuthIdx.
Then L2R is used to learn how to combine these two.
Then the user query is used to match labels of concepts and their index values are retrieved and a final top-k is returned

## Offline learning and Index construction

- ranking model
  - two features for ranking
    1. (HubScore) a concept is better the more centrail it is, the extent that the concept is related to the domain for which the ontology is formalized
    2. (AuthScore) a concept is better it it is in an authoritative ontology
  - A link analysis algorithm is used -> something like a page rank -> DualWalkRank
    - they perform link analysis independently on each ontology first and then on the whole corpus (inter-ontology links)
    - they differentiate between the type of a relationship and direction of the walk
- HubScore - score of a concept is characterized by two features
  - connectivity -> the more intra-ontology rels. starting from the concept the better
  - neightbourhood -> the more intra-ontology rels. starting from the concept to another central concept the better 
  - so it is a reverse page rank and it is iterative computation
  - the algorithm itself considers not only object-type relationships but also datatype relationships
    - they create artificial nodes for each datatype and connect it with each node that has a datatype relationship
    - they do not consider relationship weights
  - they normalize the score with z-score after the last iteration
- AuthScore - score of an ontology is characterized by two features
  - reuse -> the more links to other ontologies the better
  - neighbourhood -> links to other autohoritative ontologies are better
  - they use page rank like algorithm again where each ontology is a node
  - they again normalize the final score
  - sometimes the intra links are missing althought there are implicit imports
    - they mend the missing imports and other rels 
- DW rank score -> text relevancy, hub and authority normalized scores
  - linear ranking model
  - the text relevancy favours concepts that match multiple query words

## Query evaluation

The user inputs a query.
The concepts that match any keyword are added to a set of potential candidates (labels, comments, descritptions).
What is interesting is that they also do a "sense" matching similarity of query words and labels of concepts.