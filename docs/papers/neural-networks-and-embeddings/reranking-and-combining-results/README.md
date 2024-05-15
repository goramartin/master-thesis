# Reranking and combining results

- pseudo relevance feedback also counts as reranker

## To read

- [A Thorough Comparison of Cross-Encoders and LLMs for Reranking SPLADE](https://arxiv.org/pdf/2403.10407v1)
- [Rethink Training of BERT Rerankers in Multi-Stage Retrieval Pipeline](https://arxiv.org/abs/2101.08751)
  - appending bert to reranking is not always a good idea
- [Retrieve, Rerenk, Generate](https://arxiv.org/pdf/2207.06300v1)
  - based on [reddit](https://www.reddit.com/r/MachineLearning/comments/1286n6w/d_multilingual_retrieve_rerank_models/)
  - apperently hybrid with bm25 makes sense, and they propose it in this paper
  - also based on beir, the bi encoders dont generalize well

## For reference 

- [Reciprocal rank fusion](https://plg.uwaterloo.ca/~gvcormac/cormacksigir09-rrf.pdf) (2009)
- [Why rank level fusion.](https://www.researchgate.net/publication/276126028_Why_rank-level_fusion_And_what_is_the_impact_of_image_quality) (2015)
- [Analysis of score level fusions in deep fake detection scenarios](https://www.mdpi.com/2076-3417/12/15/7365) (2022)
- [Score level fusion in multi-biometric identification based on zones of interes](https://www.sciencedirect.com/science/article/pii/S1319157819303696) (2022)
  - Only the name, otherwise they use decision trees
- [To Interpolate or not to Interpolate: PRF, Dense and Sparse Retrievers](https://arxiv.org/pdf/2205.00235) (2021)
  - Contains references to papers about dense rerankers [10, 17, 18, 23, 24, 28, 30, 16]:
    - Expansion of the papers (most of them seem to regard colbert):
      - 10: [Efficiently Teaching an Effective Dense Retriever with Balanced Topic Aware Sampling](https://arxiv.org/abs/2104.06967) (2021)
      - 17: [Distilling dense representations for ranking using tightly-coupled teachers](https://arxiv.org/abs/2010.11386) (2021)
      - 18: [In-Batch Negatives for Knowledge Distillation with Tightly-Coupled Teachers for Dense Retrieval](https://aclanthology.org/2021.repl4nlp-1.17/)
      - 23: [ RocketQA: An optimized training approach to dense passage retrieval for open-domain question answering](https://arxiv.org/abs/2010.08191)
        - testing with doc2query, doctttttquery, gar, deepct
        - doc2query and docT5query generate questions for a document
        - gar expands questions
        - deepct learns term weight
      - 24: the same as 23 but newer
      - 28: [Approximate Nearest Neighbor Negative Contrastive Learning for Dense Text Retrieval](https://arxiv.org/abs/2007.00808) (2021)
        - they learn ann based on corpus
      - 30: [RepBERT: Contextualized text embeddings for first-stage retrieval](https://arxiv.org/abs/2006.15498)
      - 16: [Pretrained transformers for text ranking: Bert and beyond](https://arxiv.org/abs/2010.06467)
  - [Bert dense retrievers require interpolation with bm25 to be good at reranking](https://dl.acm.org/doi/10.1145/3471158.3472233) (2021)
  - Recent studies have found that interpolating sparse and dense retrieval 1 results can further enhance retrieval effectiveness [14, 17, 26], suggesting that both groups of retrievers tend to retrieve different relevant signals [14, 16]
    - 14: [A Few Brief Notes on DeepImpact, COIL, and a Conceptual Framework for Information Retrieval Techniques](https://arxiv.org/abs/2106.14807) (2021)
    - 17: [Distilling Dense Representations for Ranking using Tightly-Coupled Teachers](https://arxiv.org/abs/2010.11386) (2020)
    - 16: [Pretrained Transformers for Text Ranking: BERT and Beyond](https://arxiv.org/abs/2010.06467) (2020)
      - a survey about reranking 
  - In general the paper researches pseudo relevance feedback withing combination of sparse and dense embeddings
  - The method for vector PRF tkaes the results and combines the vectors to imporove the query vector and then queries again.
  - In this paper they test PRF before/after/both interpolation, also they aim at testing whether learned sparse embeddings and bm25 embeddings are better.
  - Other papers about combination - [1, 14, 18]
    - Expanding the papers:
      - 1: [Predicting Efficiency/Effectiveness Trade-offs for Dense vs. Sparse Retrieval Strategy Selectio](https://arxiv.org/abs/2109.10739) (2021)


## Articles 

- [Waeviate on Relative score fusion.](https://weaviate.io/blog/weaviate-1-20-release#search-re-ranking)
- [Again waeviate on Relative score fusion](https://weaviate.io/blog/hybrid-search-fusion-algorithms)
- [Distribution-Based Score Fusion](https://medium.com/plain-simple-softwaredistribution-based-score-fusion-dbsf-a-new-approach-to-vector-search-ranking-f87c37488b18)
  - on medium from waeviate
- [reranking approaches article](https://medium.com/@rossashman/the-art-of-rag-part-3-reranking-with-cross-encoders-688a16b64669)
- [SetenceTransformers scross encoding](https://www.sbert.net/examples/applications/retrieve_rerank/README.html)