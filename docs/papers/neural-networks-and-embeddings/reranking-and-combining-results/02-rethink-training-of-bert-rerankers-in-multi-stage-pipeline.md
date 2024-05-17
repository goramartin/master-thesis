# Rethink Training of BERT Rerankers in Multi-Stage Retrieval Pipeline


- [Link](https://arxiv.org/abs/2101.08751) (2021)


## Intro

Recent success with reranking using bert with bm25 scores.
And new bert models have proved to be effective as retrievers.

Intuitively a better first stage will get better second stage rerankers.
But appending the bert reranker to effective first stage retriever does not guarantee an effective final ranking.

A better candidate list causes sometimes inferior reranking.
When it improves, false positives can be hard to spot.

They introduce Localized Contrastive Estimation learning.

Experiments show that with LCE it gets better results.

## Background

Separation of efficiency was introduced due to efficiency-effectivess trade off.

B25 uses signals from texact match and can use inverted data structure.
Then bert showed a good performance on reranking and also with fine tuning

## Comments additional

- The paper it self is defining a new method of training rerankers.
- And tells that it is beneficial.