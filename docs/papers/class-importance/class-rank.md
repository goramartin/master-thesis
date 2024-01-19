# Approaches to measure class importance in Knowledge Graphs

[Link](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0252862)

### Intro

The aim of this paper is to analyze existing techniques to measure class importance and propose a new approach ClassRank (CR).
The CR is based on PR and assigns each class an importance score based on the importance of its instances.
They compare the class usage in SPARQL queries logs of different KGs.
T-BOX is a schema information for ontology building.
A-BOX is an instance information in KB.
Some methods use only T-BOX, while others use A-BOX as well.

### Importance vs Relevance

We do not have the exact definition of the importance.
Several metrics use topological features.
But there is not an approach that outperforms the rest in general.
Techniques depends on the subsequent usage.

Relevance is a purpose.
It is easier to define within a context and also is easier to evaluate.
E.g. a relevance to a given query.

While importance may be different for the creator and different for the consumers.

## Metrics

### Importance metrics applied over schema structures

The techniques used: Degreem Betweenness, Bridging Centrality, Closeness, Harmonic Centrality and Radiality.
These were used in the series of papers "s0-s3".
While here they used them only on schema (t-box) and disregarding a-box.
In this paper they use them in t-box experiments.

### Importance metrics applied over whole graph structure

Instance Counting, PageRank, HITS and ClassRank.
They use t-box and a-box together.
IC and CR need the usage of a-box, while the rest can be used on arbitrary graph.
In this paper they use HITS and PageRank on schema graph and also on entire KB.

- Instance Counting
  - class-instance relation
  - the more instances a class have the more important it is
  - wikidata apparently offer statistics about this (i found it but it is from the 2020)
  - or dbpedia offers files about instantiations
- PageRank
  - an element gains importance if it receives more links from other elements, if those links come from important elements, and if those elements have few outgoing elements
  - scores are values [0, 1]
  - it is the probability that the random surfer starting from a random node and browsing stops at particular node
- HITS
  - hub score and authority score
  - a node has a high authority score if it receives links from nodes with a high hub score
  - a node will have a high hub score when it points to nodes with a high authority score
  - the hub score is similar to page rank - a node is better if it has links with other important nodes
  - but hits and pagerank consider different importance in inciming edges.
  - the authority score aims for finding pages that link to many other important nodes
  - finds nodes from which you can jump to many other relevant nodes
  - usually it was used to compute edges over a subgraph, but here we use it on whole kb.
- ClassRank
  - the one they devised
  - The CR score of a class c consists of the aggregation of the pagerank score of its instances.
  - it quelifies the importance of a class with reference to their instances
  - they argue it is able to keep balance between the quantity and quality of those instances
  - it is the probability that a random surfer has to land in an instance of a class
  - Important comments
    - **sum of all class rank score is not 1, because score of classes with no instances, since some classes have no instances and soome classes can be subclasses of multiple classes**
      - to make it true each every node in kb should have should have exactly one class
    - ***another thing is that using only "subclass of" statement is not usually sufficient, since in a graph with people that all are subclass of a Person, would be only one important node - a Person -> to mitigate that we can propose another things like occupation or gender to provide additional classes***
      - in this paper they say, they consider multiple statements that convey the class partake
  - For the computation they use a special library for computing page rank for large graphs

### Adapted importance metrics

As in the series of papers s0-s3, the same metric for instace counting was used for metrics that did not utilize the a-boxes.

## Experiments

### Methodology

They use sparql query logs in dbpedia and wikidata as in the series of papers s0-s3.
Those lists are gold standart.
They also distinguish two traffics: human-made queries vs machine-made queries (bots).
For comparison of rankings they use Rank-Biased overlap.
A RBO is a distance measure between two rankings, where 0 means minimum distance and 1 means maximum distance.
Transforming into RBO - 1, we get 1 as maximum similarity.
It checks overlap of two rankings at incrementally increasing depths.
At each step RBO computes overlap.
Then it adds all ratios weighted using infinite series of weights whose sum converges alwasy to a fixed value.
The weight can be configured to give importance to a specific region.
Which models user persistence.

### Describing sources

- DBpedia
  - english version, spraql as text files
  - classes ranked are the ones in dbpedia ontology
  - the graph for ott techniques is the dbpedia ontology
  - they used logs 14 days straight -> each day they got the queries done in that day
  - it is almost impossible to distinguish between user queries and machine bots queries
    - normaly they would use user-agent header to detect if it was a human
    - this time they used the amount of requests in a short period of time - super human number of requests per time period
  - techniques computed
    - t-box metrics on dbpedia ontology
      - simply on schema
      - centrality + pagerank and hits
    - metrics with a-box
      - pagerank and hits and classrank
- Wikidata
  - they complained the wikidata does not define classes
  - classification on human and robot made is easy, since they distinguish it in logs
  - t-box only metrics
    - they did not do centrality
    - they used only hits and pagerank
  - a-box metrics
    - hits, pagerank, class rank
  - class pointers not only instance, but other properties do not always point to classes
    - to obtain class pointers
    - they computed every usage of a property by a ratio a property points to a class (r=0.99)

### Results

Class rank was the best.
Instances are good.


### Related work to my interest

#### Importance scores but without the ones I already have

- [PageRank on Wikipedia: Towards General Importance Scores for Entities](https://link.springer.com/chapter/10.1007/978-3-319-47602-5_41) with correlation in [Browsing DBpedia with summaries](https://link.springer.com/chapter/10.1007/978-3-319-11955-7_76) and [LinkSUM](https://www.aifb.kit.edu/images/4/43/LinkSUM.pdf)
  - the first paper uses page rank on wikipedia articles and explores the notion of imporance links within the articles
  - the other does page rank on links from dppedia
  - the third one does summaries on entities
    - they first find generally important entities and then they find strongly connected entities (how two resources are important for each other) Backlink method
    - strongly connected are based on:
      - frequency - how often is predicate used in the dataset
      - exclusivity - for both ends of relation, a movie has more than one actor while actor could play in more movies
      - description - relation are represented by rdf predicates

- [Identifying Global Representative Classes of DBpedia Ontology Through Multilingual Analysis: A Rank Aggregation Approach](https://link.springer.com/chapter/10.1007/978-3-319-68723-0_5) 
  - aggregation of score with pagerank similar to classrank based on multilingual analysis
  - they first want to find important instances
  - then they find important classes with aggregating importances of instances
  - a rank of a class for each langage is obtained by page rank values of its instances
    - the graph they worked with is a graph of instances from wikipedia consisting of links between articles and computed page rank score on it
    - rank of a class is done by mapping information between instances in Wikipedia and classes in DBpedia - using type info from DBpedia to map instances to classes
      - a class is more popular it it is ranked higher based on average of its instances scores
      - a class is more popular if it is widely populated in DBpedia a-box
      - then they for a class do aggregation with reference to instance count in specific language
  
- [Agent for Mining of Significant Concepts in DBpedia](https://link.springer.com/chapter/10.1007/978-3-642-32826-8_32) - reverse page rank on exploring neighbourhood in the graph, most related tems are the ones with low pagerank since they are very specific
  - using page rank on wikipedia
    - arguing there is no such concept of a useful page or a junk page in wikipedia
    - a page with high pagerank usually rfers to a general topic while a page with a low rank usuelly refers to a specific topic
    - is there is a link from a to b, then a should relate to concept b
  - they propose apply pagerank on dbpedia link structure by retrieving topic sensitive keywods from a specific concept based on the inverse pragerank measurement of DBpedia. Inverse means ranking related concepts based on pagerank value in ascending order
    - “find me some specific concepts that arerelevant to cat”
      - find all concepts linked to a cat page in dbpedia
      - but the more interesting concepts have a low pagerank score 

- [Explaining and suggesting relatedness in knowledge graphs](https://link.springer.com/chapter/10.1007/978-3-319-25007-6_36) - exploring relatedness explanation between two entities -> a paths that linnk those entities, they collect paths and then they can detect similar entiteis


#### Alternate centrality measures based on Pagerank

- Personalized page rank 
  - a set of restarting nodes which are the only ones that the random walker can jump to when it gets bored of following links.

- A page rank adaptations that compute relatedness between the query and resource
  - importance with combination of other notions
    - swoogle
    - [PopRank](https://www.microsoft.com/en-us/research/wp-content/uploads/2004/11/tr-2004-129.pdf)
      -  popularity link model, they argue that pagerank and hits use the equality when comming to links
      -  etending pagerank with popularity propagation factor to each link
      -  how to assign these factos? - domain experts partial rankings
      -  then they use learning methods to learn the ranks
      -  bad for wikidata because we have a lot of nodes
  - measure relevance inclusing strategies such as similarity or xploration of topic sub graph
    - [ReconRank for rdf](https://aran.library.nuigalway.ie/handle/10379/492)
      - combinatin of resourcerank and contextrank
      - the query itself collects some data and the ui displays subgraph for each resource - the results are grouped by subjects withing the rdf dataset
      - the results are dynamically rank afterwards
      - we do not have a global rankings - why? - since global scores must be recomputed every time, and pagerank is memory greedy on large datasets and global ranks maybe does not fit the query
      - a user enter keyword query - the index then returns all data matching - then we do ranking only on the topical subgraph - the result list is ranked according to popularity in the topical subgraph
      - subgraphs
        - resourcerank
          - they select inlinks and outlinks of subject node of matching literal
          - parameter n - how many hops from the match should be in the graph
          - opon the graph they do the pagerank like algorithm
        - contextrank
          - then they need context - context is provenance of data similarny constructed graph
        - then they need to combine it
          - they have links between context and resource it contains, resources abd containing context, and context to context - create a bigger grap
      - when they have the graph they compute the weighted page rank
    - [RareRank](https://www.sciencedirect.com/science/article/pii/S0020025511001198) - not for me i guess
      - they have a knowledge base
      - they plugin the a domain ontology (dont know where to take it)
      - and run some page rank like algorithm 