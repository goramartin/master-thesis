# Ontology Understanding without Tears: The Summarization Approach

[Link](https://www.semantic-web-journal.net/system/files/swj1452.pdf)

## Intro

Some Kb have a complex schemas, that hinders exploration and exploitation.
We want to highlight the most representative concepts of data sources.
They propose RDF Digest, a platform that produces and visualizes summaries of RDFS KBs.
Summary is a valid RDF graph.
Two algorithms that exploit structure and semantics of KB.
First they identify the most important nodes with notion of relevance.
Then explore how to select edges connecting these nodes by maxizing either locally or globally the importance of the selected edges.

Previously partitioning [7] and modularization [6], or building of overviews [7, 8, 9, 10, 11].
Summarization [10] is he process of distilling knowledge from an ontology in order to produce an abridged version.
What is missing is a solution for summary that uses both graph structure and semantics of KB alltogether.

They view RDFS KB as two graphs: a schema graph and instances graph.
The most important nodes have the heighest relevance: relative cardinality and in/out cardinality.
Then they try to connect them to subgraph by maximizing locally or globally the importance of selected edges.

## Assessment measures

The notion of relevance.
Previously PageRank has been used in an XML.
For RDFs are used: degree centrality, betweeness and eigenvector centrality (PageRank, HITS) adjusting them to features of RDFs or they try to adapt the degree centrality and closeness.

In this paper they believe the importance should be based on the nodes that are directly connected to it and also by reachability of this node.
A reachability of a node being able to represent effectively its neighbours.
**Nodes with a lot of connections will have a high importance.**
With respect to instances as well (more instances the better).
First they detemine how central/important a node is by the number of instances it has == **relative cardinality**, after that they use centrality of node in entire KB == **in/out centrality**.
Combination is the final relevance.

## Relative cardinality

For classes it is the number of instances.
For edges between two schema nodes, it is the number of corresponding instances of the nodes.
They also define a value if there are no instances for the edge.

## In/Out centrality

In order to combine the notion of centrality in schema and the distribution of the corresponding dataset.
It is an adaptation of the **Degree centrality** - in undirected graph, it is defined as the number of links incident upon a node.

It is defined as a sum of the weighted relative cardinality of the incoming edges, respectively, outgoing edges.
The weights are experimentaly defined.
They distringuish standart RDF types and user defined properties.
The user defined ones are more important.

## Final relevance

How central a schema nod is KB is.
It should consider also the centrality of other nodes.
It is affected by its surrounding neighbours and more specifically by the number and the connections of its adjacent nodes.
It is determined by both the connectivity in the schema and the cardinality of the instances.
Notion of relevance depicts the capability of a node to represent other nodes.

## Construction of the summary

### Selection through coverage maximization 

We want to produce valid subschema graphs.
The paths should collect the most relevant nodes by minimizing overlaps (maximize by minimize).
Two algorithms: local optimization vs global optimisation.
They define level of coverage of a specific path:
1. relevance of each node contained in the path
2. it relevnat instances in the dataset
3. length of the path

The algorithm works with coverage such that it maximizes adding paths to the summary while penalizing long paths.
The number of nodes in the graph is assigned by the user, 20% default.
So they just say, hey i want to include these top 20%, try to find paths that maximize coverage.

### Selection through relevance maximization 

We try to optimize the total importance of the deges of the summary graph.
We define relevance of an edge byt the relevance score of its endpoints.

## Evaluation

Three stages:
1. compare a part of selected ontologies with different approaches that do not have instances
2. there was missing data in other ontologies for the comparison, so they conducted user constructed summaries for the ontologies with instances
3. compare the entire graph with references

Papers to my interest:
1. [12] combining conitive, lexical and topological measures such as density and coverage -> but it marked as worse than this approach
2. [11] semiautomatic relevance + user input -> but it also measured worse than this approach
