# ARRO

[Link](https://www.semanticscholar.org/paper/2006-1-St-International-Symposium-on-Pervasive-and-Yu-Cao/dcb6af4aa7779db40a8bbc971cfdd86c1c6b7870)

They take hierarhy of the ontology into an account.
They measure semantic relations among classes and logic views of the query terms are formed.
Arro triies to automatically rank the ontologies and ceates a logic view for the query terms.

The user will use terms as input query and the ARRO will query the Swoogle service.
It then loads the ontologies and ranks them accordingly.

### Logic view of the concept

The concept is either a class, a prpoerty or comments.
The main concept is the class.
They look at the importance of the label of the class appearing in the ontology and the importance of it's relationships.

- To describe relationships they use "logic view" of a concept, LV(A) = {A°, bA, e(A)}.
    - A° - represent properties contained by A through semantic annotations (domain, range, property announced through anonmous subclass). But why? Because property represents relationships between individuals -> feature of the class. This one is the most important.
    - bA - equivalent classes - sameAs ... Why? We learn how the class is related to other ontologies and classes.
    - e(A) - other direct relations - subclassOf, intersectionOf, complementOf... Now, instance of, subclass of, superclass of describe the hierarchy and application in the real world we add eh(A). To weight them higher than other in e(A).
- The idea is that the larger LV(A) is in an ontology, the better it is.
- Query
  - matching the label directly and using its equivalence relationships.
- Ranking
  - A° should have the heighest weight, need to consider class with no properties
    - RankingValue(A) = U + |A°|, default U=1
  - since eh(A) is more important then other e(A), we give it more weight
    - they take all classes that have relation in e(A) and look and compute the score by summing up RankingValues of the classes with reference to the fact that its either the in the eh or e function
  - then they normalize it and compute weight of concept A in an ontology
  - when ranking they take a look at the frequecies of concepts in the query and compute similiraty of the query to the ontology.


