# A Thorough Comparison of Cross-Encoders and LLMs for Reranking SPLAD

- [Link](https://arxiv.org/pdf/2403.10407v1) (2024)

## Intro

In reranking, firstly there was learning to rank based on features, then bert like cross encoders came.
More architectures came encoder-decoder, encoder-only.
Now LLM are being used for effective zero shot rerankers.
RankGPT - performs well as a listwise reranker out of the box and can be incrementaly reapplied to improve the results.

But they note that baselines are not present usually when doing research with llms.
Such that if cross encoders outperform when using of strong retrievers.
Or how many documents to choose.

They want to evaluate cross encoders when reranking results from strong retrievers - in domain and out of domain.

- Results
  - cross encoder behave slightly differently when in domain vs out of domain
  - they are competitive vs llm while being more efficient
  - open llms underperform compared to gpt4

## Setting

LLMs rankers not tested on good retrievers, such as splade v3 or splade ++.
Splade v3 is the strongest model.
They choose rerankers  based on deberta v3 large and electra large.

## Datasets

In domain and out of domain.

TREC Deep leaning dataset based on MS MARCO collection.
For cross encoders they use BEIR benchmark and LoTTE as out of domain dataset.

## Results

- Cross encoders - in domain
  - obesrvations depend on the dataset
  - not conclusive which one is better
  - reordering top k =50, 100, 200
  - they show that the splade v3 benefits the most with increased 100
  - while others are stable over the k
    - since lower models will tend to retrieve documents at lower rank
  - no general trend
  - they see that the best first stage leads to the best performance

- cross encoders - out of domain
  - similar results to the in domain
  - with large enough k the models perform well
  - deberta consistently imrpoves over electra
  - they show that increasing the k is a good way to boost performance

- LLMs as rerankers
  - on pars with cross encoders
  - 

- Comparison on trec dataset
  - chat gpt performs really well with short documents
  - on cross encoder it has much more impact - and lowers performance
  - both are sensitive to titles present in the document - without it is worse

- Reranking pipeline 
  - llm is expensive
  - could be used to reorder results from cross encoderss
  - it outperforms the gpt solely and cross encoder too