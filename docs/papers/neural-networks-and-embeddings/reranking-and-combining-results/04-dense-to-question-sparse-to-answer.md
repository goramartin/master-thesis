# Dense to question and sparse to answer: hybrid retriever system for industrial frequently asked questions

[Link](https://www.mdpi.com/2227-7390/10/8/1335?trk=article-ssr-frontend-pulse_little-text-block) (2022)
  - How to normalize bm25 score when doing hybrid search.

## Intro

I found this paper thanks to a blog that noted that the min/max normalization is not that good with bm25 scores.

They focus on FAQ.
They hybridize the dense embeddings and sparse embedding to make it more robust in profesinal terms and propose weight ratio and scale the results by the two modules.

They note that they are large models for FAQ but they require large resources. So they want to focus on the traidtional retrieval with combination with dense and find a good functions to combindations.

To my work, I seek functions to combine the results.

## Scoring functions

They adopt arctangent function to normalize the scores from the architectures. 
But it is not in [0, 1] but [-1, 1]

The combination then is done using blending (lambda * normalize(dense) + (1 - lambda) * normalize(sparse))
They find out that giving more lambda to the dense is beneficial. (lambda=0.75)
