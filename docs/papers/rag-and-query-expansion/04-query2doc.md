# Query2doc: Query Expansion with Large Language Models

- [Link](https://arxiv.org/abs/2303.07678) (2023)

## Intro

Simple query expansion to imporove both sparse and dense retrieval systems.
The proposed method first generates pseudo documents by few shot prompting language.
And then expand query with the generated pseudo documents.
The method benefits even the dense retrieval.

BM25 is good and dense perform better when large amounts of labeled data are avialble.

Query expansion (Rochhio) is a long standing technique that rewrites query based on pseudo relevance feedback or external knowledge sources such as wordnet.
For sparse retrieval, it can help bridge the lexical gap between the query and the documents.
However, query expansions methods like rm3 have only shown limited success on popular datasets.
Dense retrievals do not adopt this methods.

Also methods like doc2query have proven to be effecttive for sparse retrieval.

The method is good and improves bm25, dense retrievals also benefit the method.
But it is diminishing when comparing with strong cross-encoder re-ranker.


## Method

They write a prompt with few shots and generate a passage.
There is difference for how the output is concatenated with the query.

- Sparse retrieval
  - to balance the relative weights of the query with the much longer output, they reperat the initial query multiple times (5 is generally good)
- Dense retrieval
  - they simply concatenate it with a separator

## Evaluation

The q2doc improves the methods.
There is method doct5query which is better, but it is needed to be trained specifically on the dataset.

The dense retrieval also benefits from the method, but it is much lower benefit when used with strong rerankers.

The pseudodocuments are complementary to the base query.