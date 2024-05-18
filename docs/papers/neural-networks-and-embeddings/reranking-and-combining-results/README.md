# Reranking and combining results

Usually we want to do the hybrid and fusion (interpolation) since it always gives us a better result.
Cross encoders are good.
Convex fusion is better than the rrf. Usually the higher alpha was given to the dense retriever.

## Finished

1. [A Thorough Comparison of Cross-Encoders and LLMs for Reranking SPLADE](https://arxiv.org/pdf/2403.10407v1) (2024)
   - cross encoders are on par with llms or sometimes better 
2. [Rethink Training of BERT Rerankers in Multi-Stage Retrieval Pipeline](https://arxiv.org/abs/2101.08751) (2020)
   - Sometimes with a good retriever, the hard false positive can be hard to spot -> e.g. dense retriever with cross encoder.
   - Simple bert rerankers could not fully exploit improved initial rerankings, but with new method yes
   - All in all, simple bert are not used a lot today after 4 years
   - The first paper contradicts the statement
   - While to look from another point of view, this paper just shows that simple bert is not always a good choise.
1.  [Retrieve, Rerenk, Generate](https://arxiv.org/pdf/2207.06300v1) (2022)
      - based on [reddit](https://www.reddit.com/r/MachineLearning/comments/1286n6w/d_multilingual_retrieve_rerank_models/)
      - Apperently hybrid with bm25 makes sense, and they propose it in this paper
      - Also based on beir, the bi encoders dont generalize well
      - They find the results and do the union and then pass them to cross encoder (there is no merging via rrf or something else).
      - Another proposing are [Sparse, Dense, and Attentional Representations for Text Retrieval](https://aclanthology.org/2021.tacl-1.20.pdf) 
        - By finding linear combinatoin, but did not metion the results of the lambda parameter.
        - The same as interpolation.
      - Also another one [Sparse Meets Dense: A Hybrid Approach to Enhance Scientific Document Retrieval](https://arxiv.org/abs/2401.04055) (2024)
        - They use weighted combination
        - But they dont mention whether they do it hungrily or they first retrieve the results for both models and then do the merging, it seems more that did it on the entire set.
        - Again high dense get better results around lambda 0.8 for dense
2. [Dense to question and sparse to answer: hybrid retriever system for industrial frequently asked questions](https://www.mdpi.com/2227-7390/10/8/1335?trk=article-ssr-frontend-pulse_little-text-block) (2022)
     - How to normalize bm25 score when doing hybrid search.
     - (2*arctan(x))/pi and then (lambda * n(dense) + (1-lambda) * n(sparse))
     - Larger lambda for dense was better (0.75)
     - But it does not necessarily combine the results. It seems they retrieve and then do the both to get the score disregarding wheether it was retrieved from the dense or sparse.
3. [Bert dense retrievers require interpolation with bm25 to be good at reranking](https://dl.acm.org/doi/10.1145/3471158.3472233) (2021)
   - Previously, using bm25 as first stage and rerank it with only reranker was way better then combining the scores with interpolation from the reranker.
   - They wanted to find whether it applies with bert dense retrievers.
   - The results show that interpolation is important.
   - They behave differently in terms of the interpolation in rerankers.
   - [Complement Lexical Retrieval Model with Semantic Residual Embeddings](https://arxiv.org/pdf/2004.13969) (2021)
     - Hybrid search i guess first one, but with training
     - This paper shows us that simple interpolation is better
   - [Passage Re-ranking with BERT](https://arxiv.org/pdf/1901.04085) (2020)
     - The interpolation paper was based on this one, who claims that the bert rerankers dont benefit from the interpolation with first stage bm25 score.
4. [An Analysis of Fusion Functions for Hybrid Retrieval](https://dl.acm.org/doi/10.1145/3596512) (late 2023)
   - Contains references to hybrid searchers with interpolation and rm3 expansion.
   - convex fusion (interpolation) is better in and out of domain datasets, which is show in other papers.
   - rrf falls short

## To read

## For reference 

- [Pretrained transformers for text ranking: Bert and beyond](https://arxiv.org/abs/2010.06467) (2021)
- [Utilizing BERT for Information Retrieval: Survey, Applications, Resources, and Challenges](https://arxiv.org/abs/2403.00784) (2024)
- Fusions:
  - [Reciprocal rank fusion](https://plg.uwaterloo.ca/~gvcormac/cormacksigir09-rrf.pdf) (2009)
    - The first paper proposing reciprocal rank fusion.
  - [Why rank level fusion.](https://www.researchgate.net/publication/276126028_Why_rank-level_fusion_And_what_is_the_impact_of_image_quality) (2015)
  - [Analysis of score level fusions in deep fake detection scenarios](https://www.mdpi.com/2076-3417/12/15/7365) (2022)
  - [Score level fusion in multi-biometric identification based on zones of interes](https://www.sciencedirect.com/science/article/pii/S1319157819303696) (2022)
    - Only the name, otherwise they use decision trees
  - [To Interpolate or not to Interpolate: PRF, Dense and Sparse Retrievers](https://arxiv.org/pdf/2205.00235) (2021)
    - They want to find out whether to interpolate results of hybrid search when performing Pseudo relevance feedback.
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
    - The method for vector PRF takes the results and combines the vectors to imporove the query vector and then queries again.
    - In this paper they test PRF before/after/both interpolation, also they aim at testing whether learned sparse embeddings and bm25 embeddings are better.
    - Other papers about combination - [1, 14, 18]
      - Expanding the papers:
        - 1: [Predicting Efficiency/Effectiveness Trade-offs for Dense vs. Sparse Retrieval Strategy Selectio](https://arxiv.org/abs/2109.10739) (2021)
          - They address trade-off between the cost and utility of sparse vs dense retrievers by proposing a classifier to select a suitable retrieval strategy for each query.
- [Multi-Stage Document Ranking with BERT](https://arxiv.org/abs/1910.14424) (2019)
  - The mono and duo bert.
- [RankT5: Fine-Tuning T5 for Text Ranking with Ranking Losses](https://dl.acm.org/doi/10.1145/3539618.3592047) (2023)
  - Architecture for reranking.

## Articles 

- [Waeviate on Relative score fusion.](https://weaviate.io/blog/weaviate-1-20-release#search-re-ranking)
- [Again waeviate on Relative score fusion](https://weaviate.io/blog/hybrid-search-fusion-algorithms)
- [Distribution-Based Score Fusion](https://medium.com/plain-simple-software/distribution-based-score-fusion-dbsf-a-new-approach-to-vector-search-ranking-f87c37488b18)
  - on medium from waeviate
- [Reranking approaches article](https://medium.com/@rossashman/the-art-of-rag-part-3-reranking-with-cross-encoders-688a16b64669)
- [SetenceTransformers cross encoding](https://www.sbert.net/examples/applications/retrieve_rerank/README.html)
- [Guide book](https://www.linkedin.com/pulse/guidebook-state-of-the-art-embeddings-information-aapo-tanskanen-pc3mf)
  - a guide book for retreival in 2024