# Context-driven Concept Search across Web Ontologies using Keyword Queries

[Link](https://dl.acm.org/doi/10.1145/2815833.2816958)

## Intro

Concept search that exploits structures present in ontologies and constructs contexts to effectively filter the noise in concept search results.
The main components of the approach are:

1. context for each concept extracted from relevant properties
2. query intepretation based on extracted context
3. result ranking - learning to rank

The "current" web search engines are grouped into:
1. searching for ontologies - can be coarse grained
2. searching for individuals - can be fine grained
3. searching for concepts that represent a group of individuals - best middle ground

The argue that there exist two methods of searching based on input query.
The first one is SPARQL queries but users do not want to do that.
The second one is the keyword queries - swoogle, falcons.
The second one does not capture context necessary for interpreting queries with **multiple keywords**.
The propose that ontology axioms and properties are used as contextual queries.
They extract context for each concept based on props and axioms.
They interpret query based on contexts and rank results.

## Definitions 

We have ontologies and input keywords.
Entity is a named concept or a named property.
Axiom *a* from an ontology, entities(a) is a list of entities appearing in *a*.
Function name(entity), annotations(entity) (rdfs:label, rdfs:comments, rdfs:isDefinedBy).
A context of a concept is:
 - a set of annotation values if the concept
 - entities in relevant axioms - subclass of, equivalent classes, property axioms
 - Precisely: Context(E) = name(E) ∪ annotations(E) ∪ (name(X) that are subclasses, parents, equivalent classes) ∪ (name(X) of domain and range concepts from property axioms)

## Framework

Assumption is that the input keywords are related.
They generate interpretations using these relations.
The user's intention:
    - generate implicit query interpretations such as generative language models
    - generage explicit query interpretations with clearly interpretable search results
They use the explicit interpretations using the context.

They index concept via axioms and properties in the ontology.
The context information in the index along with co-occurrence info among  keywords used in the query are used for interpretations.
The co-occurrence is done via lexical measures (more on that later).
The associations among keywords are used for query interpretation - QI.
QI evaluates direct and indirect relations among keywords are obtained from context of concept.
Then they build feature vector and learn to rank.

## Query token association

"Evaluate co-occurrence among keywords using the Pearson's Chi square measure."
Don't know what are the expected and observed values.

## Query Interpretation (QI)

Co-occurring tokens with single tokens are used to find direct relations, in which all the keywords in the query are related via properties and axioms.
Indirect relations based on expressions in equivalent and subclass axioms.
They create two sets from the input query.
1. k' a set of cooccurring and/or single terms based on the measure
2. k'' a set of keywords from query that are not in k'
Then they use cosine similarity to match(name(c) and annotations(c), k') and match(properties(c), k'').
The match function find similar concepts (somehow?).


- Direct Relation - DR(k′,k′′):=match(L(Cj ),k′) ∪ match(name(P xCj ),k′′).
  - basically we match name and annotations with the tokens from measure and the rests from properties
- Indirect Relation - i do the same direct relation match with classes that are subclasses and equivalent classes.
  - things that do not directly appear in the query but via subclass of and equivlanet class axioms

The classes matched via direct relations have the classname and its context words in the query and the indirect relations are used to extract classes that are not directly in the query.

## My comments

I think I do not understand completely how it is done in the end.
First they somehow compute the associations but dont tell how it is done exactly.
Then they find the Query interpretations but do not mention how it is used for the search.

I think I get it now.
The associations are done based on some training dataset statistics.
The interpretations are direcly using the searh in match function, but I am not sure how there are searching it since they need to compare it to every thing.


This paper has continuation in [Search and Diversification](https://link.springer.com/chapter/10.1007/978-3-319-46523-4_17)