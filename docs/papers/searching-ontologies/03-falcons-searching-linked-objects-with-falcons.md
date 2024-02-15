# Searching linked objects with falcons: approach, implementation and evaluation

[Link](https://www.researchgate.net/publication/220123904_Searching_Linked_Objects_with_Falcons_Approach_Implementation_and_Evaluation)

## Intro

A keyword-based search engine for linked objects.

- Scenarios:
  1. Keyword queries not only can describe objects but also relations between objects. A user can seek object with a link to other object. Example: "knows Tom Heath" or "IFSC demo chair". 
  2. Query "Tom Heath" and "Chris Bizer". The query returns that tom knows heath and that they both know Michael


## Keyword based search

(in the background it uses swoogle to get the ontologies)
For each object they construct virtual document that includes textual description that an inverted index from terms in vurtual documents to objects can be built.
How? By using local name and literal valued properties and entity valued properties.
They use the notion of rdf sentence to help formalize solution. Triples are b-connected if they contain common blank nodes. It is transitive. It is a minimal self-contained graph. So basically, the document contains local name, labels, predicates with they objects and literal values. All this can be put into a document vector. The assume that the terms in keyword query most likely indicate the name of the desired object directly. The document is then put into Lucene and searched using text.

## Ranking?

Fistly, objects relevant to key word query are ranked higher and popular objects are ranked higher.
- Query relevance
  - we have virtual document - and keyword query could be percieved as a document.
  - We compute similarity between two documents.
  - They take the term vector for the document which is refined by inverse document fequency. A higher weight is assigned to a term in a virtual document if the term occurs in fewer documents. But the larger documents can reduce precision. So they boost terms  from local names and labels.
- Popularity
  - they take into account in how many documents the object exists.
- Basically they put it all into a lucene and said this is the query.

## Further filtering based on class hierarchies

Class information can be in the dereference document, co-owner documnets or just documents including the object -> they say they will consider only the dereference document. They say it only works one way. That is to say, one document stating that c1 is equivalent to c2 meaning c1 is subclass of c2, does not infer that c2 is something to c1. They store the inclusion axioms and do transitive closure reasoning.

They also do recommendation of subclasses fo incremental refinement.