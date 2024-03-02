# Neural networks and embeddings



- Tools to remember
  - [natural language toolkit](https://www.nltk.org/) - for working with word net and using classical approach to linguistics


### Finished

1. [Semantic Search for Large Scale Clinical Ontologies](https://arxiv.org/abs/2201.00118) (2022)
2. [A study of concept similarity in Wikidata](https://content.iospress.com/articles/semantic-web/sw233520) (2024)
3. [Wembedder: Wikidata entity embedding web service](https://arxiv.org/abs/1710.04099) (2017)
4. [Explore Entity Embedding Effectiveness in Entity Retrieval](https://link.springer.com/chapter/10.1007/978-3-030-32381-3_9) (2019)
5. [Joint Word and Entity Embeddings for Entity Retrieval from a Knowledge Graph](https://link.springer.com/chapter/10.1007/978-3-030-45439-5_10) (2020)
6. [Exploring Summary-Expanded Entity Embeddings for Entity Retrieval](https://ceur-ws.org/Vol-2482/paper7.pdf) (2018)
7. [Graph-Embedding Empowered Entity Retrieval](https://arxiv.org/abs/2005.02843) (2020)
8. [Entity Embeddings for Entity Ranking: A Replicability Study](https://link.springer.com/chapter/10.1007/978-3-031-28241-6_8) (2023)
9. (brief) [BERT-ER: Query-specific BERT Entity Representations for Entity Ranking](https://www.semanticscholar.org/paper/BERT-ER%3A-Query-specific-BERT-Entity-Representations-Chatterjee-Dietz/95786e847d7d73911f3718cf59408ad9a9d5beb8) (2022)
10. [Entity-aware Transformers for Entity Search](https://arxiv.org/abs/2205.00820) (2022)
11. (brief)[ Inductive Representation Learning on Large Graphs](https://arxiv.org/abs/1706.02216) (2018)
12. (brief)[ ERNIE: Enhanced Language Representation with Informative Entities](https://arxiv.org/abs/1905.07129) (2019)
13. (brief)[ E-BERT: Efficient-Yet-Effective Entity Embeddings for BERT](https://arxiv.org/abs/1911.03681) (2019)
14. (brief)[ KEPLER: A Unified Model for Knowledge Embedding and Pre-trained Language Representation](https://arxiv.org/abs/1911.06136) (2020)
15. [Generating Explainable Abstractions for Wikidata Entities](https://wikidataworkshop.github.io/2022/papers/Wikidata_Workshop_2022_paper_8269.pdf) (2021)
16. [Combining Text Embedding and Knowledge Graph Embedding Techniques for Academic Search Engines](https://ceur-ws.org/Vol-2241/paper-08.pdf) (2018)

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
    - in general not good for entity retrieval and search
    - widely used for its easy interpretation
  - [Complex Embeddings for Simple Link Prediction](https://www.semanticscholar.org/paper/Complex-Embeddings-for-Simple-Link-Prediction-Trouillon-Welbl/2218e2e1df2c3adfb70e0def2e326a39928aacfc)
    - a better than transE based on complex number
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