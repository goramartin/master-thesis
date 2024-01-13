# Novel Node Importance Measures to Improve Keyword Search over RDF Graphs

[Link](https://link.springer.com/chapter/10.1007/978-3-030-27618-8_11)

### Intro

The importance in graphs is typically computed using centrality measures that depend on the degree of nodes, such as PageRank.
But in RDF graphs the notion of importance is not always related to the node degree.
This paper proposes a way to define importance in RDF graphs and how to use it to compile and rank results of keyword queries.

The query over RDF graph is formalized as a minimal subgraph of the RDF graph that covers the keywords.
Its premise is to complete three main tasks in RDF keyword search:
1. finding pieces of information in the rdf graph
2. assemble the retrieved pieces of information to compose complete answers
3. rank the answers
In the WIR the ranking should rank the documents not only based on how well they match the keywords but also based on the importance of the documents.
The existing approaches use centrality measures for hyperlinks - PageRank and HITS.
They assign high scores to pages that are referenced by many other important pages.
This paper argue that the variations of PR or HITS work well, since the incoming and outgoing edge indicate relevance of resource.
But RDF-KwS operate over full RDF graphs, where this does not necessarily indicate  nodes importance with respect to any existing node relationships, or it may be hard to detect which relationships would express importance -> A movie database with instances of "common classes" have high number of incoming edges, but this does not mean they are important.
So in this paper:
1. How to define importance that is not related to degree
2. How to use the importance in ranking.

They define measures InfoRank:
1. important things have lots of information about them
2. important things are surrounded by other important things
3. few important relationshipt are better than many unimportant relations
Benefits -> they do not need manual assignment of weights or training dataset.

What papers are regarding the related work?
- Variations of the algs to add links [12, 15, 18, 21, 26]
- Manually weighting links [3, 20, 29]
- Machine learning [1, 24, 27]
- ObjectRank [3] was the first to use PageRank for computing importance in RDB
- Swoogle used pageRank too.
- TripleRank used tensors and decomposition but it s hard to extend for keyword search and it is slow for large datasets
- FORK weights of links by user relevance
- Closeness centrality for undirected graphs  [14] -> it is not efficient for large graphs
- [22] degree decoupled pageRank -> penilize or boost importance of node degree in recommendation graphs

### Importance measures in general

The simplest importance measure is to analyze its degree, but it is a local importance which is not ideal in some contexts.
We want global analysis.
1. For example Betweenness Centrality which counts the number of shortest paths going though a node, hence it is able to identify notable connectors.
2. Closeness Centrality measures the average distance from a node to all other nodes, hence the more cental a node is, the closer it is to all other nodes.
3. "it is not about what you know, but who you know", how well the node is connected to other important nodes. 
   1. PageRank for using hyperlinks. 
     - If pages has links from other important nodes, that the page is also important
     - computation using iterative method Power Iteration

### Info rank intuition

1. important things have lots of information about them
    - more important nodes have more literals thourgh datatype properties
    - a movie with international projection have a lot of literals, and labels in many languages
2. important things are surrounded by other important things
   - titanic actors
   - they argue that properties usually have it is inverse, so they assume the RDF graph is undirected and consider all neighbours of a node when propagating, **but i disagree with that**
3. few important relationships are better than many unimportant relations
   - in introduction they said that many importance measures depend on node degree
   - but here they do not want to boost or penilize degree importance but focus on a strategy that favours quality of relation rather then quantity

### Ranking

- Instance informativeness
  - they focus first on instance informativeness since the instances have usually more literals
  - the more literals the better
- Class informativeness
  - important classes usually have informative instances and important properties are usually those connecting informative instances
  - they define it as the maximum value of its instances informativeness
  - they sort it descendingly
- Property informativeness
  - is the maximum sum of (instance + class informativeness)
  - basically take a look at the triples
  - they sort it descendingly

- Ranking
  - they use intuition 1 to rank metatada
  - but use all three to rank instances and blank nodes
  - we define weight of a node r (instance or blank node) and property p as the normalization of all properties on r
  - then they use the page rank as usuall but with the weights on properties assuiming undirected graph
  - the final rank for instances is the sum of its informativeness and the page rank score

### Keyword search system

An answer of a keyword query over an rdf graph is one or more minimal subgraphs that cover all keywords.

The naive approach:
1. find nodes that match the keywords
2. find minimal steiner tree (minimal tree that encompasses a all vertices from a given set)
3. if there is more than one answer, rank them

Why is it bad?
The set of nodes matching keywords can be too large and computing a minimal steiner problem is NP complete.
To minimize these problesm they use a tool QUIOW.
The tool explores schema information. 
The schema is in a form of a graph.
QUIOW groups keywods matches around classes.
In other words, it identifies properties whose values match keywords and creates groups of properties that have the same class as domain.
In the second state, it finds steiner tree for the set of classes found before.
Then they use SPARQL query to synthesized to compute the answer of keyword query.

In this work they maintain the idea of grouping matches ni classes/properties to generate the SPARQL template.
But they reformulate the creation to allow use of InfoRank.

### Finding info in RDF graph

Algorithm that takes keywords and returns the best se of class/property groups.
They said that they already have the groups compute.
And just iterate over the groups prioritizing things with higher text matches and info rank scores.

### Connecting and ranking

They want to create a Steiner tree with the classes of the groups found in previous step.
The steiner tree is computed over the schema graph.
This step generates another template.
Then everything is put into a sparql query which returns the final triples.


### Final comments

To my use case, the searching does not seem very beneficial.
The aim of this paper was to mainly search over general data in RDF with the focus on instance data.
The schema was not used a lot.