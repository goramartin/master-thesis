# Estimating Node Importance in Knowledge Graphs Using Graph Neural Networks

- [Link](https://dl.acm.org/doi/abs/10.1145/3292500.3330855) (2021)

## Intro

How to estiname node importance?
In this paper they focus on setting, when they are given some importance scores of some nodes in kg.
Some can be significance or popularity of a node in the KG.
Then given a KG, how can they predict a node importance by making use of importance scores **known for some nodes** along with auxiliary information in Kgs such as edge types?

The first solution was a pagerank, but it is based solely on the graph structure and unaware of importance scores available for some nodes.
Then a personalized paged rank dealt with this limitation by letting users provide their own notion of importance, but it does not take edge types into an account.
Then a HAR comes, which distinguishes between different predicates in KGs while being aware of importance scores and graph topology.
But there see there is a room for improvement.

Previously, the solutions were not trainable based on the authors prior assumptions about the model.
In this paper they explore the solutions for the task of predicting node importance in KGs, namely, regularized supervised machine learning algorithms.
They mostly focus on GNN.

There were challenges of GNN how to model relationship between importance of neighboring nodes, estimation accross different type of entities.

They present a GENI - gnn for estimating node importance in kgs.
It is attentive gnn for predicate aware score aggregation to capture relations between the importance of nodes and their neighbours.
It allows flexible score adjustment according to node centrality which captures connectivity of a node in terms of graph topology.

## My reflection

Based on the problem definition:

- Definition 2.1 (Node Importance Estimation). Given a KG G = (V , E = {E1, E2, . . . , EP }) and importance scores {s} for a subset Vs ⊆ V of nodes, learn a function S : V → [0, ∞) that estimates the importance score of every node in KG.

For a given KG with some nodes having importance scores, they approach the importance esimation problem by developing a supervised framework learning a function that maps any given node in kg to its score, such that the estimation reflects its true importance as closely as possible.

Also they model in-domain and out-of-domain estimations. In-domains meaning that given importance scores for a set of nodes of given type, they learn estimation only for the type.
Out-of domain are estimations that are not the given type.

It seems that they want to learn estimation and I am not sure how to use it for the search.