# Neural networks and embeddings

- Tools to remember
  - [natural language toolkit](https://www.nltk.org/) - for working with word net and using classical approach to linguistics
  - KGTK

### Finished

1. [Semantic Search for Large Scale Clinical Ontologies](https://arxiv.org/abs/2201.00118) (2022)
   - Finding concepts in large ontologies can be challenging when queries use different vocabularies.
   - A search algorithm that overcomes this problem in situations where concepts can be referred to in different ways.
   - They use deep learning based approach to build search system.
   - They propose Triple-BERT and a meethod that generates training data directly from ontologies.
    - They used only labels and trained with the triple loss function so that the concepts close in the ontology (is a) were close with the embeddings. 
   - They need tp gather data - but they use additional paper that enables them to generate the data.
2. [A study of concept similarity in Wikidata](https://content.iospress.com/articles/semantic-web/sw233520) (2024)
   - One of the most influcential paper.
   - They want to explore concept similarity in the wikidata - since it is community driver - has errors.
   - They claim that previous methods focused on direct tasks, and similarity in KBs is understudied, but in linguistics it is popular.
   - They use graph embeddings, text embedding models, ontology based metrics as initial similairyt estimators.
   - They also concatenate embeddings. Also they use retroffiting of vectors -> area of classes combined into a vector.
   - They also consider human generated abstract from dbpedia and do their own lexicalization for language models.
       1. node labels
       1. node descriptions
       2. is-a values
       3. has properties
       4. property values
   - Language models performed the best, it is important what information should be considered. Labels did not do very good but with description it was best.
   - Combination proved to be not that simple (appending vectors). It is better to get a good two models than more unreliable models. 
3. [Wembedder: Wikidata entity embedding web service](https://arxiv.org/abs/1710.04099) (2017)
   - Creating a word2vec model from sentences that were formed from triples.
   - Relies only on item to item properties. 
4. [Explore Entity Embedding Effectiveness in Entity Retrieval](https://link.springer.com/chapter/10.1007/978-3-030-32381-3_9) (2019)
   - Ad-hoc entity retrieval aims to answer user querries throught returning entities from kb.
   - Three models - text match, entity mention and embedding model. Also learning to rank to combine the results.
     - FSDM
     - Entity linking incorporated retrieval model.
     - Embedding as TransE since it has a good explainability.
   - Candidates with FSDM top 100. Learning to rank also. TransE from cpp.
   - Embeddings does the best job in imporoving the retrieval - the most wieght was in the transE and entity linking (as in [7]).
   - The weight distribution showed that the transE has the most weight of all.
5. [Joint Word and Entity Embeddings for Entity Retrieval from a Knowledge Graph](https://link.springer.com/chapter/10.1007/978-3-030-45439-5_10) (2020)
   - Previously models for ad-hoc entity retrieval based on direct term matching which suffer from mismatch between vocabularies in entities and in queries.
   - Documents are not the best since they lack graph structure.
   - Graph embeddings are good for link prediction and with walk learning do not consider text.
   - They create a method that utilizes walks and creates sentences based on the walks.
6. [Exploring Summary-Expanded Entity Embeddings for Entity Retrieval](https://ceur-ws.org/Vol-2482/paper7.pdf) (2018)
   - Mentiones that when trying to reuse task specific entity embeddings for retrieval, results can be less than impressive. Like rdf2vec for datamining but is worse than bm25. Fully deep models exists but they do not have enough data.
   - They propose that entity embeddings are based on other entities.
   - They link entities from dbpedia abstract and create embeddings.
   - Vocam mismatch is a problem.
   - The hypotetize that mapping the query to entity space and comparing with entities will ipmprove results.
   - First term based model for candidates.
   - Word to vec models, and combinations.
   - They are agains query expansion.
7. [Graph-Embedding Empowered Entity Retrieval](https://arxiv.org/abs/2005.02843) (2020)
   - Two stage retreival.
   - They obtain results with bm25.
   - Then they locate entity mentions in the query.
   - And do combination of the similarity of the entities from query to the result sets with interpolation of the bm25 score. EMbedding based reranking from linking do not perform well enough. But combination yest. Graph based embeddings were better tha context only. 
   - Based on tagme and wikipedia (dbpedia).
   - The problem with this solution is that we dont have the tool on wikidata and the data is not there -> see entity linking directory.
8. [Entity Embeddings for Entity Ranking: A Replicability Study](https://link.springer.com/chapter/10.1007/978-3-031-28241-6_8) (2023)
   -  Replication of [7] anc combining it with ERNIE and E-BERT (knowledge enchanced models).
   -  Find that embeddings are beneficial.
9.  (brief) [BERT-ER: Query-specific BERT Entity Representations for Entity Ranking](https://www.semanticscholar.org/paper/BERT-ER%3A-Query-specific-BERT-Entity-Representations-Chatterjee-Dietz/95786e847d7d73911f3718cf59408ad9a9d5beb8) (2022)
    - the aspect hell
    - dont want to look at it again
10. (brief) [EM-BERT Entity-aware Transformers for Entity Search](https://arxiv.org/abs/2205.00820) (2022)
    - Pretrained models fail when doing complex reasoning over entities.
    - It is combination of e-bert and mono bert.
    - Recently enhanced knowledge from graph of entities.
    - They explore enrichment of entities for retrieval.
    - Finetuning leads to instabilities and not enough data.
    - Combining kg embeddings.
    - They transform wikipedia2vec entity embeddings into bert word piece space and use them as input to the bert model.
    - They do a linear transformation.
    - We dont have enough data for this. And needs learning.
11. (brief)[ Inductive Representation Learning on Large Graphs](https://arxiv.org/abs/1706.02216) (2018)
    - A paper about graph embeddings that can work with texts. Used in neo4j.  
12. (brief)[ ERNIE: Enhanced Language Representation with Informative Entities](https://arxiv.org/abs/1905.07129) (2019)
    - They train language model and kgs.
    - They recognize entity mention in text and then they align these mentions to their entities in kgs.
      - Embeddings transE.  
    - Then they adopt mask language model and next sentence predition as pretrianing.
13. (brief)[ E-BERT: Efficient-Yet-Effective Entity Embeddings for BERT](https://arxiv.org/abs/1911.03681) (2019)
    - They align Wikipedia2Vec entity vectors with bert's native wordpiece vector space and use the aligned entity vectors as if they were wordpiece vectors.
    - They dont want to do the pretraining as in ERNIE.
14. (brief)[ KEPLER: A Unified Model for Knowledge Embedding and Pre-trained Language Representation](https://arxiv.org/abs/1911.06136) (2020)
    - It integrates factual knowledge into plms but produce effective text enhanced ke with strong plms.
    - They encode textual entity descriptions with plm as their embeddings, and then jointly optimize the ke and lm objectives of ke and mlm.
    - They encode text and entities into the unified space with the same plm encoder.
    - For ke the objective, they encode entity descriptions and then train them with the conventional methods for ke.
    - For the mlm they use existing approach.  
    - It is good for unseen entities.
15. [Generating Explainable Abstractions for Wikidata Entities](https://wikidataworkshop.github.io/2022/papers/Wikidata_Workshop_2022_paper_8269.pdf) (2021)
    - In this paper, they investigate how to define abstractive representations of entities.
    - They propose a method that produce profiles for wikidata entities based on salient labels associated with theri types. 
    - Not for my usecase, since it is for instances and not classes.
16. [Combining Text Embedding and Knowledge Graph Embedding Techniques for Academic Search Engines](https://ceur-ws.org/Vol-2241/paper-08.pdf) (2018)
    - A simple search engine working with text embeddings for search and kg embeddings for searching similar entities after a user selects a specific entity.  
17. [BEIR](https://arxiv.org/abs/2104.08663) 
    - benchmark for retrieval

### To read

### For reference

- KGTK library papers and references:
  - [Hybrid Structured and Similarity Queries over Wikidata plus Embeddings with Kypher-V](https://wikidataworkshop.github.io/2022/papers/Wikidata_Workshop_2022_paper_7722.pdf) (2022)
    - KGTK library for kg exploration, aims at using graph queries with embeddings (similar to neo4j) for analysis of kgs.
    - But aims at constructing the new query language and finding the most similar entities based on graph embeddings.
  - [KGvec2go – Knowledge Graph Embeddings as a Service](https://aclanthology.org/2020.lrec-1.692.pdf) (2020)
    - Ccreating and serving api for wikidata entities using rdf2vec, similar to webembedder on wikidata.
    - The main idea was to create a service so others could access the embeddings witout the need to create them themselves.
    - They took the model and datasets and trained it on the data and then provided the interface.
  - [User-friendly Comparison of Similarity Algorithms on Wikidata](https://www.semanticscholar.org/paper/User-friendly-Comparison-of-Similarity-Algorithms-Ilievski-Szekely/0f21f87dc9460356627d6ac7c53cc92d19233d4d) (2021)
    - From KGTK comparisons for similarity of entities in wikidata, the paper is cited in the Wikidata similarity of concepts.
    - Focuses on graph embeddings when we hold an entity and then they compare the graph embeddings.
- Benchmarks:  
  - [MTEB](https://arxiv.org/abs/2210.07316)
- A bit of general theory:
  - [BERT](https://arxiv.org/abs/1810.04805)
  - [S-BERT](https://arxiv.org/abs/1908.10084) 
    - including cross encoders
  - [Utilizing BERT for Information Retrieval: Survey, Applications, Resources, and Challenges](https://arxiv.org/abs/2403.00784) (2024)
  - [Dense Text Retrieval based on Pretrained Language Models: A Survey](https://arxiv.org/abs/2211.14876)
    - a great intro into the dense retrievals
    - contains info abou architectures as well
  - [Knowledge Graph Embedding: A Survey of Approaches and Applications](https://ieeexplore.ieee.org/document/8047276) (2017) and the more new [A Survey of Knowledge Graph Embedding and Their Applications](https://arxiv.org/abs/2107.07842) (2021)
  - [SPLADE: Sparse Lexical and Expansion Model for First Stage Ranking](https://arxiv.org/abs/2107.05720) (2021)
      - a new state of the art method for candidate generation using sparse vectors
      - more on sparse vectors [sparse](https://qdrant.tech/articles/sparse-vectors/)
  - [Translating Embeddings for Modeling Multi-relational Data](https://www.semanticscholar.org/paper/Translating-Embeddings-for-Modeling-Data-Bordes-Usunier/2582ab7c70c9e7fcb84545944eba8f3a7f253248) (2013)
    - transE for modeling link predictions
    - the idea is that for the triples, the translation should be the closest tail or head
    - it is used in the ERNIE knowledge induced things of wembedder
    - in general not good for entity retrieval and search
    - widely used for its easy interpretation
  - [Complex Embeddings for Simple Link Prediction](https://www.semanticscholar.org/paper/Complex-Embeddings-for-Simple-Link-Prediction-Trouillon-Welbl/2218e2e1df2c3adfb70e0def2e326a39928aacfc)
    - a better than transE based on complex number
  - [Fielded Sequential Dependence Model for Ad-Hoc Entity Retrieval in the Web of Data](https://www.semanticscholar.org/paper/Fielded-Sequential-Dependence-Model-for-Ad-Hoc-in-Zhiltsov-Kotov/607a834558b16c318be9c735bea048ae6638841d) (2015)
    - some model rival of bm25
    - a good introduction to the older models
    - there are few mentions how to construct a fielded entity that was used in other papers
      - names
      - attributes
      - categories
      - similar entity names
      - related entity names
- Knowledge enhanced language models:
  - [Knowledge Enhanced Pretrained Language Models: A Compreshensive Survey](https://www.semanticscholar.org/paper/Knowledge-Enhanced-Pretrained-Language-Models%3A-A-Wei-Wang/290867638c5ca520de5c48aa4336f196d426c226) (2021)
  - [A Survey of Knowledge Enhanced Pre-trained Language Models](https://arxiv.org/abs/2211.05994) (2022)
  - [KELM: Knowledge Enhanced Pre-Trained Language Representations with Message Passing on Hierarchical Relational Graphs](https://arxiv.org/abs/2109.04223) (2022), there is also KEPLET model
     -  for incorporating kg into language models
- Recommendations:
  - [A Comparative Study of Text Embedding Models for Semantic Text Similarity in Bug Reports](https://arxiv.org/abs/2308.09193) (2023)
  - prompting fine tuned model [GenRec: Large Language Model for Generative Recommendation](https://arxiv.org/abs/2307.00457) (2023)
  - [Recommendation as Language Processing (RLP): A Unified Pretrain, Personalized Prompt & Predict Paradigm (P5)](https://arxiv.org/pdf/2203.13366.pdf) (2022)
- Od krystofa
  - [Word Embeddings for Wine Recommender Systems Using Vocabularies of Experts and Consumers](https://www.ronpub.com/ojwt/OJWT_2018v5i1n04_Cruz.html) (2018)
  - [Learning Word Embeddings from Wikipedia for Content-Based Recommender Systems](https://link.springer.com/chapter/10.1007/978-3-319-30671-1_60) (2016)