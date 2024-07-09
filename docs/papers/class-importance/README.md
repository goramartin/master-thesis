# Class importance and/or summarization

The aim of this research was find a way to model importance of classes in knowledge graphs.
It also coalesce with another problem, summarization, which aims at labeling certain concepts the most importance and then provides a summary based on the top x % from the entire graph. 
The idea is also to use the summaries as a means of explorations.

In summary, the general ideas convert around network analysis (centrality and spectral analysis) and instance of information (number of instances per class).
The solution are trying to model importance in the knowledge graphs.
I argue that this topic is not of great importance to me, since the metric are based on node degrees and general pathways in the graph.
E.g. number of edges between nodes, number of children or number of parents.
I believe this does not reflect user's intentions when he wants to model using a dataspecer.
Just not to forget: the best methods used pagerank, hits or number of instances per class.

- What to take from this?
  - methods that are trying to define importance but for different aim [as stated in 7]
  - pagerank, hits, and instance information carry the most value
  - almost every method is based on network analysis and degree of the nodes (page rank and hits)
  - there is also personalized and reversed pagerank
  - mention things like axioms of centrality, number of instances, number of inlinks and outlinks in wikidata (sitelinks)
  - some people work with query logs and looked for class information in them - such as class usage in queries to define importance as a gold standart
- Possible future work?
  - try multiple reranking algorithms based on centrality and spectral analysis, just for the sake of it

### Finished

1. [CAR-rank: Identifying Potentially Important Concepts and Relations in an Ontology](https://www.semanticscholar.org/paper/Identifying-Potentially-Important-Concepts-and-in-Wu-Li/4f713a8b72dafa9bfdb64bb967f1e96de5156775) (2008)
   - the idea is that they model importance as a view from the authors view as he was modeling the ontology
   - they compute wieghted reverse page rank while updating edge weights
   - the problem with this approach is that they assume that important concepts have more edges, while i argue that it might not be a good option for the modeling the user wants to do in the dataspecer
   - since even if the class do not have a lot of edges, it still  can be important to the user for modeling
2. [Info-rank: Novel Node Importance Measures to Improve Keyword Search over RDF Graphs](https://link.springer.com/chapter/10.1007/978-3-030-27618-8_11) (2019)
   -  this belongs to the domain of keyword search over rdf graphs, as in the one of the topics in the index
   -  they define the problem as a minimum subgraph of of the knowledge graphs
   -  they want to find importance that is not based on node degree and how to use it in ranking
   -  they say the node is more important the more literals it has (which is also a degree), nodes connected to important nodes are better and few important rels are better then a lot of unimportant
   -  the aim was to do a sparql query in the end
3. s0-[Ontology Understanding without Tears: The Summarization Approach](https://www.semantic-web-journal.net/system/files/swj1452.pdf) (2016)
   - They want to highlight the most representative concepts of data sources.
   - They view RDFS KB as two graphs: a schema graph and instances graph.
   - The most important nodes have the heighest relevance: relative cardinality and in/out cardinality.
   - Then they try to connect them to subgraph by maximizing locally or globally the importance of selected edges.
   - In the end they combine number of instances per class and the degree of the nodes
   - they rely on the log of queries to db pedia to evaluate the methods
4. s1-[Exploring Importance Measures for Summarizing RDF/S KBs](https://link.springer.com/chapter/10.1007/978-3-319-58068-5_24) (2017)
   - continuation form previous
   - the idea is to try use the certain centrality metrics that combine metric based on the number of instances 
   - they say it is much better than the previous ones 
   - betweeness centrality was the best one 
5. s2-[Exploring RDFS KB using summaries](https://trepo.tuni.fi/bitstream/handle/10024/105166/exploring_rdfs_2018.pdf?sequence=1) (2018)
   - mostly trying to explore the kb with zoom in and out operations on the summaries
   - they also add spectral metrics for the importances - pagerank and hits
6. s3-[SumMER: Structural Summarization for RDF/S KGs](https://www.mdpi.com/1999-4893/16/1/18) (2022)
   - combining the centrality and specral measurements to gain better understanding of what is important
   - pagerank, hits and number of instances had the most weight
   - modeling as a regression problem based on dbpedia query logs
7. [Class-Rank: Approaches to measure class importance in Knowledge Graphs](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0252862) (2022)
   - The CR is based on PR and assigns each class an importance score based on the importance of its instances. 
   - They compare the class usage in SPARQL queries logs of different KGs.
   - additional papers inside my comments
   - Several metrics use topological features, but there is not an approach that outperforms the rest in general. It is easier to define within a context and also is easier to evaluate  
8. [Estimating Node Importance in Knowledge Graphs Using Graph Neural Networks](https://dl.acm.org/doi/abs/10.1145/3292500.3330855) (2021)
   - it is important to note here, that the main point is the estimation
   - they assume someone already gave them the importance scores for a subgraph and their work is to predict scores for other nodes 

### To read

- [Identifying Key Concepts in an Ontology, through the Integration of Cognitive Principles with Statistical and Topological Measures](https://link.springer.com/chapter/10.1007/978-3-540-89704-0_17) (2008)

### For reference

- [Axioms for Centrality v2](https://vigna.di.unimi.it/ftp/papers/AxiomsForCentrality.pdf) (2020 new print)
  - axioms describing centrality in networks
  - contains general math explanations and theory
  - also contains which method fulfil the axioms
- [Graph based methods survey](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8527452) === [Ontology summarization: Graph based methods and byond](https://www.worldscientific.com/doi/abs/10.1142/S1793351X19300012) (2019)
  - general methods on summarizations
- [Entity summarization: State of the art and future challenges](https://www.sciencedirect.com/science/article/pii/S1570826821000226) (2021)
- [Ontology summarization based on rdf sentence graph](https://dl.acm.org/doi/10.1145/1242572.1242668) (2007)
  - using weighted hits, pagerank and focused pagerank (similarty of a concept to the ontology) also includes reranking to obtain better coverage
- [Workload based summaries](https://dl.acm.org/doi/pdf/10.1145/3468791.3468815) (2021)
  -  importance based on usage in queries, similar to the evaluation in the s0-3 series of papers
