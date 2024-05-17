# Bert dense retrievers require interpolation with bm25 to be good at reranking

- [Link](https://dl.acm.org/doi/10.1145/3471158.3472233) (2021)

## Intro

A common approach to retreival is to create first stage bm25 with pseudo relevance feedback and then use bert to rereank the top bm25 k passages (often 1000) [5, 9, 17]

An implementation decision when implementing the bert reranker is if it should use the ouput scores from bert alone or combine them with the original bm25 scores.

Some studies point out that that bm25 score is ignored when using the bert reranking. (not retriever now)
They go futher that exact term matching scores do not provide any relevance signals that is not already captured by bert.

It is unclear whether it applies to the bert based dense retrievers.
There was a paper [10] that does interpolation at inference time.

They provide empirical investigation of the importance of interpolating bert and bm25 scores for those bert dense retrievers that do not consider bm25 during training and inference.

They show that this interpolation provides significant gains in effectiveness compared to using the bm25 or dr scores alone.

They also show that drs not interpolated with bm25, perform poorly with respect to deep evaluation measures.

Why? 
Since dr are better at modelling strong releenace signals than bm25.

## Do DR encode the same relevance signals as BM25

They do the query bm25 and then dense retrievers separately and then do the interpolation - if some is missing it gains 0.
Taking the top 1000.
The procedure is follwed in [12] as well.

When doing search with only dr it gets better results than bm25.
At least in the shallow evaluations here.
It first appears to be the same as in [14].

They show that the interpolation improved over only dense and onnly sparse.
When more power was given to the dense embeddings.

## Interpolation results on deep evaluation measures.

They show that using dr alone is not provide always better results.
Combination is better with 0.5 for interpolation.
Even for systems that are designed to do so.

## Uppoer bound on interpolation.

tunig 0.5 gains a good results.

## Comments

- Previously, using bm25 as first stage and rerank it with only reranker was way better then combining the scores with interpolation from the reranker.
- They wanted to find whether it applies with bert dense retrievers.
- The results show that interpolation is important.
- They behave differently in terms of the interpolation in rerankers.