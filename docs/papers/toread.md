# Search frameworks and ontology ranking

### Finished

1. Swoogle: A Search and Metadata Engine for the Semantic Web (2004)
2. WATSON: a gateway for the semantic web (2007)
3. Searching linked objects with falcons: approach, implementation and evaluation (2009)
4. Ranking Ontologies with AKTiveRank (2006)
5. Ontology Evaluation and Ranking using OntoQA (2007)
6. Linked Open Vocabularies (LOV): A gateway to reusable semantic vocabularies on the Web (2017)
7. ARRO: Novel Approach for Ranking Ontologies on the Semantic Web (2006)
8. Ontology-rank - Ontology selection ranking model for knowledge reuse (2011)
9. OS-Rank - Ranking Ontology Based on Structure Analysis (2009)
10. Content-based Ontology Ranking  (2006)
11. Content-OR:  An Integrated Ontology Ranking Method for Enhancing Knowledge Reuse (2014)
12. Context-driven Concept Search across Web Ontologies using Keyword Queries (2015)
13. DWRank - Learning Concept Ranking for Ontology Search (2016)

### To read

### To read but with less interest

### For reference

- OntoSelect, OntoKhoj (2008)
  - popularity based the more references to other o. the better.

- [Popularity driven Ontology ranking using Qualitative features](https://orbilu.uni.lu/bitstream/10993/40972/1/2019-07-02_iswc19-ranking-final.pdf) (2019)
  - CARRank, Termpicker, CBRBench, Word2Vec-> popularity based on citations per year and linear trend in citations history, not important to me, but it has a good introduction citating interesting papers and benchmarks

- [Ranking Schemas by Focus](https://www.researchgate.net/publication/353514217_Ranking_Schemas_by_Focus_A_Cognitively-Inspired_Approach) (2021)
  - defines class importance based on cathegorization of properties on a node (domains). This could be usefull, the problem is how to combine it with the number of properties is wikidata. Also they say it works well with noisy schemas and compare it with TF-IDF, BM25, CMM and DEM.

- [LOD search engine: A semantic search over linked data](https://link.springer.com/article/10.1007/s10844-021-00687-0) (2021)

- ELECTRE
  -  [A comparative application of multi criteria decision making in ontology ranking](https://link.springer.com/chapter/10.1007/978-3-030-20485-3_5) (2019)
     -  i used this to obtain the good searchers
  - [Comprative ranking of ontologies with ELECTRE](https://www.researchgate.net/publication/365607097_Comparative_Ranking_of_Ontologies_with_ELECTRE_Family_of_Multi-criteria_Decision-Making_Algorithms) (2022)
    - 2022 using complexity metrics for evaluation of ontologies based on CRank (Complexity ranking methods)
  - [CRank](https://link.springer.com/chapter/10.1007/978-3-030-00856-7_7) (2018)
    - complexity metrics

# Class importance and/or summarization

### Finished

1. CAR-rank: Identifying Potentially Important Concepts and Relations in an Ontology (2008)
2. Info-rank: Novel Node Importance Measures to Improve Keyword Search over RDF Graphs (2019)
3. s0-Ontology Understanding without Tears: The Summarization Approach (2016)
4. s1-Exploring Importance Measures for Summarizing RDF/S KBs (2017)
5. s2-Exploring RDFS KB using summaries (2018)
6. s3-SumMER: Structural Summarization for RDF/S KGs (2022)
7. Class-Rank: Approaches to measure class importance in Knowledge Graphs (2022)
  - additional papers inside my comments

### To read

- [Identifying Key Concepts in an Ontology, through the Integration of Cognitive Principles with Statistical and Topological Measures](https://link.springer.com/chapter/10.1007/978-3-540-89704-0_17) (2008)


### For reference

- [Axioms for Centrality v2](https://vigna.di.unimi.it/ftp/papers/AxiomsForCentrality.pdf) (2020 new print)
  - axioms describing centrality in networks
  - contains general math explanations and theory
  - also contains which method fulfil the axioms
- [Graph based methods survey](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8527452) === [Ontology summarization: Graph based methods and byond](https://www.worldscientific.com/doi/abs/10.1142/S1793351X19300012) (2019)
  - general methods on summarizations
- [Ontology summarization based on rdf sentence graph](https://dl.acm.org/doi/10.1145/1242572.1242668) (2007)
  - using weighted hits, pagerank and focused pagerank (similarty of a concept to the ontology) also includes reranking to obtain better coverage
- [Workload based summaries](https://dl.acm.org/doi/pdf/10.1145/3468791.3468815) (2021)
  -  importance based on usage in queries, similar to the evaluation in the s0-3 series of papers
- Importance 
  - [Estimating Node Importance in Knowledge Graphs Using Graph Neural Networks](https://dl.acm.org/doi/abs/10.1145/3292500.3330855) (2021)

# Ontology mapping

### Finished

### To read maybe

- [Background knowledge in ontology matching](https://www.semantic-web-journal.net/content/background-knowledge-ontology-matching-survey-0) (2022)
  - good matchers are using BERT models just LLM
  - KGMatcher from google is good or WiktionaryMAtcher 


### For reference

- [OLaLa: Ontology Matching with Large Language Models](https://arxiv.org/abs/2311.03837) (2023)
  - they create embeddings for all classes in the ontology via sentence bert and lexicalization of properties
  - then they find candidates with sentence bert
  - then they ask large language model whether the text are the same
  - and they look for response in the model prompt

# Necasky

### Finished

1. KNIT: Ontology reusability through knowledge graph exploration

### To read

- [RAG](https://www.linkedin.com/posts/jbarrasa_advanded-rag-with-knowledge-graphs-ugcPost-7139723682007920640-q9cA)

# Neural networks and embeddings

### Finished

1. Semantic Search for Large Scale Clinical Ontologies (2022)
2. A study of concept similarity in Wikidata (2024)
3. Wembedder: Wikidata entity embedding web service (2017)
4. Explore Entity Embedding Effectiveness in Entity Retrieval (2019)
5. Joint Word and Entity Embeddings for Entity Retrieval from a Knowledge Graph (2020)
6. Exploring Summary-Expanded Entity Embeddings for Entity Retrieval (2018)

### To read

- Regarding Wikidata
  - [Generating Explainable Abstractions for Wikidata Entities]((https://wikidataworkshop.github.io/2022/papers/Wikidata_Workshop_2022_paper_8269.pdf)) (2021)
  
- General things
  - [Entity Embeddings for Entity Ranking: A Replicability Study](https://link.springer.com/chapter/10.1007/978-3-031-28241-6_8) (2023)
  - [Graph-Embedding Empowered Entity Retrieval](https://arxiv.org/abs/2005.02843) (2020)
  - [BERT-ER: Query-specific BERT Entity Representations for Entity Ranking](https://www.semanticscholar.org/paper/BERT-ER%3A-Query-specific-BERT-Entity-Representations-Chatterjee-Dietz/95786e847d7d73911f3718cf59408ad9a9d5beb8) (2022) should be better then E-BERT
  - [E-BERT: Efficient-Yet-Effective Entity Embeddings for BERT](https://www.semanticscholar.org/paper/E-BERT%3A-Efficient-Yet-Effective-Entity-Embeddings-Poerner-Waltinger/2bd5b4aed18400bf1a1cc866d9b8d931aa047290) (2019)


- Continuation
  - maybe [Autoregressive Entity Retrieval](https://www.semanticscholar.org/paper/Autoregressive-Entity-Retrieval-Cao-Izacard/572c12e81319ccd47cc0c637c82efadd03fd05ab) (2020)
  - maybe [Learning Dense Representations for Entity Retrieval](https://www.semanticscholar.org/paper/Learning-Dense-Representations-for-Entity-Retrieval-Gillick-Kulkarni/6b5cb3b85fb247256b264c2732916cf129015a92 (2019)
  - maybe [Zero-shot Entity Linking with Dense Entity Retrieval](https://www.semanticscholar.org/paper/Zero-shot-Entity-Linking-with-Dense-Entity-Wu-Petroni/592a6691373f3936631bc4ac122f69df09c842bd) (2019)

### For reference

- General
  - [Fielded Sequential Dependence Model for Ad-Hoc Entity Retrieval in the Web of Data](https://www.semanticscholar.org/paper/Fielded-Sequential-Dependence-Model-for-Ad-Hoc-in-Zhiltsov-Kotov/607a834558b16c318be9c735bea048ae6638841d) (2015)
    - some older model rival of bm25
    - there are few mentions how to construct a fielded entity that was used in other papers
  - [SPLADE: Sparse Lexical and Expansion Model for First Stage Ranking](https://arxiv.org/abs/2107.05720) (2021)
    - a new state of the art method for candidate generation using sparse vectors
- Recommendations
  - [A Comparative Study of Text Embedding Models for Semantic Text Similarity in Bug Reports](https://arxiv.org/abs/2308.09193) (2023)
  - prompting fine tuned model [GenRec: Large Language Model for Generative Recommendation](https://arxiv.org/abs/2307.00457) (2023)
  - [Recommendation as Language Processing (RLP): A Unified Pretrain, Personalized Prompt & Predict Paradigm (P5)](https://arxiv.org/pdf/2203.13366.pdf) (2022)
- Od krystofa
  - [Word Embeddings for Wine Recommender Systems Using Vocabularies of Experts and Consumers](https://www.ronpub.com/ojwt/OJWT_2018v5i1n04_Cruz.html) (2018)
  - [Learning Word Embeddings from Wikipedia for Content-Based Recommender Systems](https://link.springer.com/chapter/10.1007/978-3-319-30671-1_60) (2016)

# Keyword search over Knowledge graphs

This sounds like something very close to my topic, but the resulting operation is somewhat returning the subgraph containing all the keywords.
It seems that the first phase is to locate all the keywords matching and then building some sort of Steiner-Tree problem for constructing the minimal subgraph. 

- surveys
  - this one is the most important [A systematic literature review and classification of approaches for keyword search over graph-shaped data](https://www.semantic-web-journal.net/content/systematic-literature-review-and-classification-approaches-keyword-search-over-graph-shaped) (2023)
  - [Keyword search on large graphs: A survey](https://link.springer.com/article/10.1007/s41019-021-00154-4) (2021)