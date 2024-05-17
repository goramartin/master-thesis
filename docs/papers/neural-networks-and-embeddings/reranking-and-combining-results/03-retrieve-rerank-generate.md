# Re2G: Retrieve, Rerank, Generate

- [link](https://aclanthology.org/2022.naacl-main.194/) (2022)
  - based on [reddit](https://www.reddit.com/r/MachineLearning/comments/1286n6w/d_multilingual_retrieve_rerank_models/)
  - apperently hybrid with bm25 makes sense, and they propose it in this paper
  - also based on beir, the bi encoders dont generalize well

## Intro

They want to continue with RAG and neural retriever.
They combine both neural retriever and reranking into bard-sequence-to-sequence generation.
They also permit ensemble of BM25 and neural initial retrieval.
Using the scores from reranker, they can find the top k results from union of dense and sparse results.
At inference time the query is encoded using the DPR query encoder and the top-12 passages from the HNSW index are returned. 
The query is also passed to BM25 search, specifically Anserini5, gathering the top-12 BM25 results. 
Both sets of passages are passed to the reranker and scored.

Otherwise they train the models.

From my perspective, the ensemble part is interesting to my work.

A good mention is that bert models provided state of the art agains leraning to rank models.

## Additinal comments

Results from initial state can be greatly improved by reranking [Liu, 2009 (first learning to rank), Wang et all 201 (cascade model for retrieval)].
Scores of bm25 are not comparable to the inner products from dpr.
Using the scores from reranker, they can find the top k documents from the union of dpr and bm25.

They merge the results by scoring the resuls by their inverse rank from each method.
Even the simple solution improves the ranking.