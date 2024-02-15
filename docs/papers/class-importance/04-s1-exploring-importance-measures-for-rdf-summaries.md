# Exploring Importance Measures for Summarizing RDF/S KBs (2017)

[Link](https://link.springer.com/chapter/10.1007/978-3-319-58068-5_24)

## Intro

The paper is continuation of the previous approach in "ontology without tears".
We want to understand and explore RDF KBs by summarization.
Question is how to find the most important nodes and then how to link them.
They revise 6 measures from graph theory and then proceed to linkage of the nodes.
They want the most important parts of the schema.
The linkage is a Steiner Tree problem.
They split the KB into two parts: schema graph and instances graph (as in "Understanding without tears").

## Importance measures

There is no universal accepted measurement on the importance of nodes in an RDF graphs.
They take a look at 6 measures that were previously proposed.
And then they show how they adapted the measurements to consider instance information.
The measures are: Betweeness, Bridging Centrality, Degree, Harmonic Centrality, Radiality and Ego Centrality.
They are state-of-the-art measures for generic graphs [2].
They do not compare with spectral measures (HITS, PageRank), because they are based on the external factos and spectral properties.

1. Degree
  - A number of edges incident to the node
2. Betweenness
  - is equal to the number of shortest paths from all nodes to all other nodes that pass through that node
  - ! but i am not sure how this works in directed graphs.. the thing is we have only the hierarchy and domains
3. Bridging centrality
  - tries to indentify information flow and topological locality of a node in network
  - it is used for clustering or finding spots interrupting information flow
  - a node with high score is connecting densely connected components in a graph
4. Harmonic centrality
  - initially defined for undirected graphs
  - it is modificatoin of the closeness, replacing the average distance with harmonic mean of all distances
6. Radiality
  - how close a node is to all other nodes in a graph
7. Ego Centrality
  - for a node v, EC is induced subgrapg, wichi contains v, its neighbours and all the edges between them
  - tells us how important a node is to its neighbours

## Adapting the measures for instances

Firstly, they normalize each importance measure.
Secondly, they normalize each the number of instances that belong to a schema node.
The adapted measures are the sum of the normalized importance measure and the number of instances for the thing.

## Evaluation of importance measures

They do not want to rely on domain experts.
So they exploit the query logs from DBpedia endpoinds trying to identify the schema nodes that are more frequently queried.
The most important ones are the that have higher frequency of appeaance in the queries.
We define direct and indirect appearance of a class inside query.
- Direct
  - when a class appears directly inside the query triple (SPARQL)
- Indirect
  - a class is type of an instance or domain/range of a property that appear in the triple pattern
They say that the paper outperforms importance measures from previous approaches "ontology without tears" and previous version of the RDFdigest.

## Final Comment

The paper states that the methods used here in importance metrics outperforms previous measurements in the "ontology without tears".
The best metric was betweeness in DBPedia.
Problem with this is that we have oriented graph.
And that the things are not combined into one.