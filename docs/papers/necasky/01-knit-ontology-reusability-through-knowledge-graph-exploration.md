# KNIT: Ontology reusability through knowledge graph exploration

[Link](https://www.sciencedirect.com/science/article/pii/S0957417423007418)

## Intro

A tool KNIT for exploration of open repositories to help users fetch previously designed concepts using keywords.
The topis is finding concepts in ontologies (multiple ontologies).
The users inputs a query with keywords, classes and relations are extracted and then a draft KG populated with the concepts abd relationships retrieved from existing ontologies.
After the first draft is created it is further refined with ontology learning algorithms -> development of new KB.
The premise is reuse of ontologies for creation of new ontologies.

Construction of new KG is hard.
Reusing existing concepts is hard as well, since there is heterogenity of existing conceptualisations and the availability of ontologies.
One of metodologies for creation argue that the process must follow seven fundamental steps:
1. determine a domain and scope
2. consider reuse
3. list essential terms in the ontology
4. define classes and hierarchies
5. define properties of classes
6. define facets
7. create instances
Another methodology is to reuse existing ontologies and reuse as much terms from the selected ontology -> coherence.
A lot more steps for creation of ontologies.
A lot of ontologies are not designed to be reused or be found in general.

For my use case, it seems that only the part regarding search and selection is interesting.

## What is KNIT?

Knowledge recycling networks.
They propose methods to find and rank existing concepts in existing knowledge structures, given a domain context.
Analyse thier interconnection and relationships and representing them with a KG.
And then further use those concepts to create new ontology by transforming them to an ontology.

## KNIT Framework

KNIT takes a list of keywords as input and produces an OWL ontology importing the reused artefacts as a results.
It has 4 steps:
1. retrieve concepts
   - matching 1:0..1 to concepts from all source ontologies in the repository
   - the repository must allow
     - retrieve a ranked list of matching concepts and their provenance given a single input term
     - retrieve all parents of a concept in ontology
     - retrieve equivalent classes
     - retrieve all properties of a class
   - for each term they record only the first cnadidate conceptt ranked by similarity from each of source ontologies -> candidate concepts
2. ranking and selection
   - they rerank candidate concepts according to coverage of their source ontologies in descending order
   - coverage is the number of candidate concepts retrieved from a single source ontology
   - then they assigned a top candidate to each input ermss with non empty candidate list
   - if there is a tie -> more properties per concept is better
3. building taxonomy
   - for the selected concept set they recursively retrieve parent concepts from the source ontologies
   - the retreieved parents and taxonomy rels. are included in the structure
   - iterations goes from the selected in descending order -> the process stops if a root, a thing node or a newly retrieved parent node has an equivalent node among other selected nodes and already retrieved parent nodes 
4. enrichment
   - for each node of the new taxonomy -> retrieve properties from the source ontologies
5. resulting owl

## Use cases - Knowledge graph exploration

A 5 page showing input and resulting graphs.

## Evaluation

The final graphs are unknown -> subjective measure is needed.
They propose two synthetic use cases.
They select two ontologies that have a llot of connections to other ontologies.
They take one ontology and put it in a black list, subsequently they use terms from the blacklisted ontology as input query and try to recreate it.
The evaluation is then done with regard to similarity of the blacklisted ontology with the newly created ontology.

Ovarlap of the two ontologies are done using Jaccard coefficient for similarity of two sets.
But they need to know what classes and properties mean the same thing.
There are ontology matching algorithms but they chose a manual process.




