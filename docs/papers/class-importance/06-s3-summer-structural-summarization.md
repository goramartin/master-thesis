# SumMER: Structural Summarization for RDF/S KGs

[Link](https://www.mdpi.com/1999-4893/16/1/18)

## Intro

This paper is a continuation of a previous on "exploring kbs using summaries".
In this parer again the main point is to assess importance of classes, get the best ones and subsequently build a schema sub graph as in previous papers.
The difference is that this time, they try to combine the metrics with machine learning to get a better view on importance.

The metrics used: the degree, the bridging, and the harmonic centrality, the radiality, the ego centrality, the betweenness, the PageRank and the HITS, each one of them perceiving differently the importance of the available nodes.

Which is the combo from previous papers.
They model the problem of selecting top-k as the regression problem.
Each node gets a set of features based on centrality measures and correspinging number of instances.

## Evalutation

As previously, they rely on query log with the idea that the important classes are the most used in the queries.
Wikidata has a query log available -> but does not allow schema extraction.
The heighest ranked things in the regressions were HITS, PageRank and the number of instances. 
The best regression method was Decision Trees.