# Search frameworks and ontology ranking

### Finished
- Order as time went  
  - swoogle 
  - watson 
  - falcons 
  - aktiverank
  - onto-qa
  - lov
  - arro
  - ontology-rank (or)
  - os-rank
  - content-based
  - content-or
  - context-driven
  - dw-rank

### To read

### To read but with less interest

### For reference

- OntoSelect, OntoKhoj  
  - popularity based the more references to other o. the better.

- [Popularity driven Ontology ranking using Qualitative features](https://orbilu.uni.lu/bitstream/10993/40972/1/2019-07-02_iswc19-ranking-final.pdf) 
  - CARRank, Termpicker, CBRBench, Word2Vec-> popularity based on citations per year and linear trend in citations history, not important to me, but it has a good introduction citating interesting papers and benchmarks

- [Ranking Schemas by Focus](https://www.researchgate.net/publication/353514217_Ranking_Schemas_by_Focus_A_Cognitively-Inspired_Approach) 
  - 2021, defines class importance based on cathegorization of properties on a node (domains). This could be usefull, the problem is how to combine it with the number of properties is wikidata. Also they say it works well with noisy schemas and compare it with TF-IDF, BM25, CMM and DEM.

- [LOD search engine: A semantic search over linked data](https://link.springer.com/article/10.1007/s10844-021-00687-0) 

- ELECTRE
  -  [A comparative application of multi criteria decision making in ontology ranking](https://link.springer.com/chapter/10.1007/978-3-030-20485-3_5) 
     -  i used this to obtain the good searchers 2019
  - [Comprative ranking of ontologies with ELECTRE](https://www.researchgate.net/publication/365607097_Comparative_Ranking_of_Ontologies_with_ELECTRE_Family_of_Multi-criteria_Decision-Making_Algorithms) 
    - 2022 using complexity metrics for evaluation of ontologies based on CRank (Complexity ranking methods)
  - [CRank](https://link.springer.com/chapter/10.1007/978-3-030-00856-7_7)
    - complexity metrics

# Class importance and/or summarization

### Finished

- car-rank
- info-rank
- s0-ontology-without-tears
- s1-exploring-importance-measures
- s2-exploring-kbs-using-summaries
- s3-summer
- class-rank
  - additional papers inside my comments

### To read

- [Identifying Key Concepts in an Ontology, through the Integration of Cognitive Principles with Statistical and Topological Measures](https://link.springer.com/chapter/10.1007/978-3-540-89704-0_17)


### For reference

- [Axioms for Centrality v2](https://vigna.di.unimi.it/ftp/papers/AxiomsForCentrality.pdf)
- [Graph based methods survey](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8527452) === [Ontology summarization: Graph based methods and byond](https://www.worldscientific.com/doi/abs/10.1142/S1793351X19300012)
- [Ontology summarization based on rdf sentence graph](https://dl.acm.org/doi/10.1145/1242572.1242668)
  - using weighted hits, pagerank and focused pagerank (similarty of a concept to the ontology) also includes reranking to obtain better coverage
- maybe [Workload based summaries](https://dl.acm.org/doi/pdf/10.1145/3468791.3468815) 
  -  importance based on usage in queries, similar to the evaluation in the s0-3 series of papers

# Ontology mapping

### Finished


### To read

- [Background knowledge in ontology matching](https://www.semantic-web-journal.net/content/background-knowledge-ontology-matching-survey)

# Necasky

### Finished

- KNIT: Ontology reusability through knowledge graph exploration

### To read

- [RAG](https://www.linkedin.com/posts/jbarrasa_advanded-rag-with-knowledge-graphs-ugcPost-7139723682007920640-q9cA)

# Neuronky

### To read

I am trying to include some sort of preference...

- [Semantic Search for Large Scale Clinical Ontologies](https://arxiv.org/abs/2201.00118) 
  - and it has complementary paper [Self-learning ontological concept representation for searching and matching](https://www.semanticscholar.org/paper/Self-learning-ontological-concept-representation-Ngo-Koopman/6985beaffc63602f8978e0c58cf7855c089adc9c)

- Importance 
  - [Estimating Node Importance in Knowledge Graphs Using Graph Neural Networks](https://dl.acm.org/doi/abs/10.1145/3292500.3330855)


- Regarding Wikidata
  - [A study of concept similarity in Wikidata](https://content.iospress.com/articles/semantic-web/sw233520)
  - [Generating Explainable Abstractions for Wikidata Entities](https://wikidataworkshop.github.io/2022/papers/Wikidata_Workshop_2022_paper_8269.pdf)
  - [Joint Word and Entity Embeddings for Entity Retrieval from a Knowledge Graph](https://link.springer.com/chapter/10.1007/978-3-030-45439-5_10)
  - [Wembedder: Wikidata entity embedding web service](https://www.semanticscholar.org/paper/Wembedder%3A-Wikidata-entity-embedding-web-service-Nielsen/d62c1d88d8ecf80e3e1efee1c659e21ea050202d)

- Od krystofa
  - [Word Embeddings for Wine Recommender Systems Using Vocabularies of Experts and Consumers](https://www.ronpub.com/ojwt/OJWT_2018v5i1n04_Cruz.html) 
  - [Learning Word Embeddings from Wikipedia for Content-Based Recommender Systems](https://link.springer.com/chapter/10.1007/978-3-319-30671-1_60)

- Nauronky a recommendations
  - for reference [A Comparative Study of Text Embedding Models for Semantic Text Similarity in Bug Reports](https://arxiv.org/abs/2308.09193)
  - prompting fine tuned model [GenRec: Large Language Model for Generative Recommendation](https://arxiv.org/abs/2307.00457)
  - [Recommendation as Language Processing (RLP): A Unified Pretrain, Personalized Prompt & Predict Paradigm (P5)](https://arxiv.org/pdf/2203.13366.pdf)


# Keyword search over Knowledge graphs

This sounds like something very close to my topic, but the resulting operation is somewhat returning the subgraph containing all the keywords.
It seems that the first phase is to locate all the keywords matching and then building some sort of Steiner-Tree problem for constructing the minimal. 

- surveys
  - this one is the most important [A systematic literature review and classification of approaches for keyword search over graph-shaped data](https://www.semantic-web-journal.net/content/systematic-literature-review-and-classification-approaches-keyword-search-over-graph-shaped)
  - [Keyword search on large graphs: A survey](https://link.springer.com/article/10.1007/s41019-021-00154-4)

- Some old papers might not need to read these
  - [Keyword search on graph based on content and structure](https://link.springer.com/chapter/10.1007/978-3-319-07782-6_68)
    -  alg. which considers not only the structure of the distance between the nodes, but also the similarity between node and query in searching phase 
  - [Semantic-driven keyword search over knowledge graphs](https://ceur-ws.org/Vol-2798/paper3.pdf)
    - The focus is particularly on enhancing the accuracy of subgraph ranking by leveraging semantic in- formation combined with other factors. Preliminary results demonstrate that the combination of importance-based and semantics-based metrics is promising compared to purely structural techniques