# WATSON: a gateway for the semantic web

[Link](https://www.researchgate.net/publication/48989644_WATSON_a_gateway_for_the_semantic_web)

The paper seems like a list of ideas to implement but it does not describe the solutions. I picked only few ideas.

### Intro

A tool and an infrastructure that automatically collects, analyses and indexes ontologies and semantic data available online. Unlike Swoogle it takes into account and exploits the particularities of Semantic Web. Such as:
- considering only explicit relations - does not check for duplicities
- weak notion of semantic quality - swoogle uses only popularity, but quality can be as important
- weak access to semantic content - bad interface -> Ontosearch2

### Analyzing semantic content

- labels, comments, what vocabularies/languages were used, information about entities, quality of the doc
- relationships to other docs - explicit (imports) and implicit, they focus on equivalence to tackle duplicities

### Advanced ontology selection mechanisms

- dont use only string similarity but use semantics info to match the concepts
- use quality measurements - structural, topic relevance ...

### Topic-based Ontology Organization

- use topic based queries