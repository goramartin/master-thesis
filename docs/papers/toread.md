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
- [Entity summarization: State of the art and future challenges](https://www.sciencedirect.com/science/article/pii/S1570826821000226) (2021)
- [Ontology summarization based on rdf sentence graph](https://dl.acm.org/doi/10.1145/1242572.1242668) (2007)
  - using weighted hits, pagerank and focused pagerank (similarty of a concept to the ontology) also includes reranking to obtain better coverage
- [Workload based summaries](https://dl.acm.org/doi/pdf/10.1145/3468791.3468815) (2021)
  -  importance based on usage in queries, similar to the evaluation in the s0-3 series of papers
- Importance 
  - [Estimating Node Importance in Knowledge Graphs Using Graph Neural Networks](https://dl.acm.org/doi/abs/10.1145/3292500.3330855) (2021)

# Ontology mapping

### Finished

### To read maybe

- [Knowledge graph embedding methods for entity alignment: experimental review](https://link.springer.com/article/10.1007/s10618-023-00941-9)
  - bert_int method is the best

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
7. Graph-Embedding Empowered Entity Retrieval (2020)
8. Entity Embeddings for Entity Ranking: A Replicability Study (2023)
9. (brief) BERT-ER: Query-specific BERT Entity Representations for Entity Ranking (2022)
10. Entity-aware Transformers for Entity Search (2022)
11. (brief) Inductive Representation Learning on Large Graphs (2018)
12. (brief) ERNIE: Enhanced Language Representation with Informative Entities (2019)
13. (brief) E-BERT: Efficient-Yet-Effective Entity Embeddings for BERT (2019)
14. (brief) KEPLER: A Unified Model for Knowledge Embedding and Pre-trained Language Representation (2020)
15. Generating Explainable Abstractions for Wikidata Entities (2021)
16. Combining Text Embedding and Knowledge Graph Embedding Techniques for Academic Search Engines (2018)

### To read

- RAG
  - [Retrieval-Augmented Generation for Large Language Models: A Survey](https://arxiv.org/abs/2312.10997)
    - first retrieve results
    - then ask the llm for ranking or selecting
    - does not have to read it all, just learn what others did
- Query expansion
  - [Query Expansion by Prompting Large Language Models](https://arxiv.org/abs/2305.03653) (2023)
    - unlike traditional pseudo relevance they use llm
    - try different prompts
    - it is more powerful than the traditional methods
  - [Query2doc: Query Expansion with Large Language Models](https://arxiv.org/abs/2303.07678) (2023)
    - the method generates pseudo documents by few shot prompting and then expands the query with generated pseudo documents

### For reference

- Sparse retrieval as first step
  - [Knowledge Graph Embedding: A Survey of Approaches and Applications](https://ieeexplore.ieee.org/document/8047276) and the more new [A Survey of Knowledge Graph Embedding and Their Applications](https://arxiv.org/abs/2107.07842)
  - [SPLADE: Sparse Lexical and Expansion Model for First Stage Ranking](https://arxiv.org/abs/2107.05720) (2021)
    - a new state of the art method for candidate generation using sparse vectors
- General
  -  [KELM: Knowledge Enhanced Pre-Trained Language Representations with Message Passing on Hierarchical Relational Graphs](https://arxiv.org/abs/2109.04223) (2022), there is also KEPLET model
     -  for incorporating kg into language models
  - [Knowledge Enhanced Pretrained Language Models: A Compreshensive Survey](https://www.semanticscholar.org/paper/Knowledge-Enhanced-Pretrained-Language-Models%3A-A-Wei-Wang/290867638c5ca520de5c48aa4336f196d426c226) (2021)
  - [A Survey of Knowledge Enhanced Pre-trained Language Models](https://arxiv.org/abs/2211.05994) (2022)
  - [Translating Embeddings for Modeling Multi-relational Data](https://www.semanticscholar.org/paper/Translating-Embeddings-for-Modeling-Data-Bordes-Usunier/2582ab7c70c9e7fcb84545944eba8f3a7f253248) (2013)
    - transE for modeling link predictions
    - the idea is that for the triples, the translation should be the closest tail or head
    - it is used in the ERNIE knowledge induced things of wembedder
  - [Complex Embeddings for Simple Link Prediction](https://www.semanticscholar.org/paper/Complex-Embeddings-for-Simple-Link-Prediction-Trouillon-Welbl/2218e2e1df2c3adfb70e0def2e326a39928aacfc)
    - a better than transE
  - [Fielded Sequential Dependence Model for Ad-Hoc Entity Retrieval in the Web of Data](https://www.semanticscholar.org/paper/Fielded-Sequential-Dependence-Model-for-Ad-Hoc-in-Zhiltsov-Kotov/607a834558b16c318be9c735bea048ae6638841d) (2015)
    - some older model rival of bm25
    - there are few mentions how to construct a fielded entity that was used in other papers
- Recommendations
  - [A Comparative Study of Text Embedding Models for Semantic Text Similarity in Bug Reports](https://arxiv.org/abs/2308.09193) (2023)
  - prompting fine tuned model [GenRec: Large Language Model for Generative Recommendation](https://arxiv.org/abs/2307.00457) (2023)
  - [Recommendation as Language Processing (RLP): A Unified Pretrain, Personalized Prompt & Predict Paradigm (P5)](https://arxiv.org/pdf/2203.13366.pdf) (2022)
- Od krystofa
  - [Word Embeddings for Wine Recommender Systems Using Vocabularies of Experts and Consumers](https://www.ronpub.com/ojwt/OJWT_2018v5i1n04_Cruz.html) (2018)
  - [Learning Word Embeddings from Wikipedia for Content-Based Recommender Systems](https://link.springer.com/chapter/10.1007/978-3-319-30671-1_60) (2016)

# Entity linking to Wikidata

It is the task of linking entity mentions to Wikidata entities.
This could be used in the query analyzation process.
E.g. finding entity mentions (classes and properties in the query and then do someething like similarity).
The aim is to find something that could be used directly.

### Finished

1. OpenTapioca: Lightweight Entity Linking for Wikidata (april 2019)
2. Falcon 2.0: An Entity and Relation Linking Tool over Wikidata  (december 2019)
3. Improving Candidate Retrieval with Entity Profile Generation for Wikidata Entity Linking (2022)
4. Encoding Knowledge Graph Entity Aliases in Attentive Neural Network for Wikidata Entity Linking (2020)
 
### To read

- [CHOLAN: A Modular Approach for Neural Entity Linking on Wikipedia and Wikidata](https://arxiv.org/abs/2101.09969) (2021)
- [Tweeki: Linking Named Entities on Twitter to a Knowledge Graph](https://aclanthology.org/2020.wnut-1.29/) (2020)
  - unsupervised
  - tagger from allen nlp library
  - To adapt Intrawiki links to the WikiData KB, we use the existing links between Wikipedia and WikiData entities to gather all the entity aliases and number of time each alias is used in Wikipedia for the entity
  - code is missing only the data are present

### For reference

- [ReFinED: An Efficient Zero-shot-capable Approach to End-to-End Entity Linking](https://arxiv.org/abs/2207.04108)
  - can be used with wikidata and the code seems maintained
  - this seems like a good option
- [A Neural Approach to Entity Linking on Wikidata](https://link.springer.com/chapter/10.1007/978-3-030-15719-7_10) (april 2019)
  - this paper is a predecesor of Falcon 2
  - in falcon 2 they argue that neural methods do not have enough data for training
  - in this paper specifically focus only on disambiguation and not recognition, thus it is hard to use
- [Scalable Zero-shot Entity Linking with Dense Entity Retrieval](https://aclanthology.org/2020.emnlp-main.519/)
  - for wikipedia only BLINK
- [NECKAr: A Named Entity Classifier for Wikidata](https://link.springer.com/chapter/10.1007/978-3-319-73706-5_10)
  -  In this paper we present the tool NECKAr, which assigns Wikidata entities to the three main classes of named entities.

# Keyword search over Knowledge graphs

This sounds like something very close to my topic, but the resulting operation is somewhat returning the subgraph containing all the keywords.
It seems that the first phase is to locate all the keywords matching and then building some sort of Steiner-Tree problem for constructing the minimal subgraph. 

- surveys
  - this one is the most important [A systematic literature review and classification of approaches for keyword search over graph-shaped data](https://www.semantic-web-journal.net/content/systematic-literature-review-and-classification-approaches-keyword-search-over-graph-shaped) (2023)



