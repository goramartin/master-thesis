# BEIR

- [Link](https://arxiv.org/abs/2104.08663) 

We leverage a careful selection of 18 publicly available datasets from diverse text retrieval tasks and domains and evaluate 10 state-of-the-art retrieval systems including lexical, sparse, dense, late-interaction and re-ranking architectures on the BEIR benchmark. 
Our results show BM25 is a robust baseline and re-ranking and late-interaction based models on average achieve the best zero-shot performances, however, at high computational costs. 
In contrast, dense and sparse-retrieval models are computationally more efficient but often underperform other approaches, highlighting the considerable room for improvement in their generalization capabilities. 

Previously BM25 and other methods good for text matching but dense are better for understanding.
But training them is tedious and intensive so they are used in zero shot manner.

It is uncleat how well the learned systems generilize in domain and out of domain.

They find out that no systems outperfroms all.
They find out that in domain performance does not correlate well with its generalization capabilities.
And that dense retrievers can underperform vs bm25.
Models finetuned with idntical training data might geneealize differently.
Reranking models and late interactino models perform the best but are expensive.
more efficient approach based on dense or spase can underperform traditional lexical models, and they remain as strong baselines.
They also generalize well.

(Shows intro to bm25 and why is it used and also that cross encoders are good but expnsive.)