# LLMs and RAG

- RAG:
  - the naive rag to question what is the best thing to ask and ask for reranking
  - retrieval strategies
    - preretrival
      - adding the right data to the embedding
      - aligments - how to distinguish between the similar concepts, (hypotetical question)
      - finetuning embeddings
        - baii
        - similar to triple bert
        - there must be a need to generate data
      - dynamic embeddings (bert like models)
    - reranking before placing it into a prompt
      - lost in the middle phenomenon
      - diversity ranking
      - recalculating semantic similarity (keep the order)
    - working with the query
      - generate necessary context for the query - there could be an option for including cathegory
      - create pseudo document before retrieval
      - create multiple queries before retrieval and rerank them
      - query2doc, hyde,  rrr, step backprompting
  - dont forget llm specific things
    - some llms prefer different inputs
    - most of the things need a lot of data

- Query expansion and rewring
  - the baseline is rm3 but it is not used often and lacks 
  - prompting llms to get better results
  - i wanted to generate:
    - terms for the query
    - or entire sample document
    - the generation would need the probably some sort of context, this could be inputet by the user
  - query2doc and [query expansion by prompoting] are good things
  - backstep prompting to get abstract reasoning
  - hyde needs learning
  - rrr quering web and reinforcement leaning, but there is also version wihout reinforcement leanrning 

- Named entity recognition?
  - Dominik does this
  - would there be a way to find out about the named entities in the text?
  - there would have to be a sentence or just prompts
  - there might not be the need for named entity recognition and relation
  - i could just rewrite it all together
  - it would be bad for keyword queries

- terms not to forget 
  - chain of thought
  - rewriting
  - few shot prompting

### Finished

1. [RAG](https://www.linkedin.com/posts/jbarrasa_advanded-rag-with-knowledge-graphs-ugcPost-7139723682007920640-q9cA) (ongoing)
     - [youtube](https://www.youtube.com/playlist?list=PL9Hl4pk2FsvX-5QPvwChB-ni_mFF97rCE)
     - It is showing us the differences between graph similarity and vector similarity and how to combine them.
     - The ideas are demostrated on the neo4j (which i wanted to use in the end as well).
     - They mostly demostrate the ideas with rag on generating outputs with augmented context, I would like to search the entities with the rag.
     - something like here is the list of 1000 entities, give me the top 20
2. [Retrieval-Augmented Generation for Large Language Models: A Survey](https://arxiv.org/abs/2312.10997) (last revisited january 2024)
    - first retrieve results
    - then ask the llm for ranking or selecting
    - does not have to read it all, just learn what others did
3. [Query Expansion by Prompting Large Language Models](https://arxiv.org/abs/2305.03653) (2023)
    - unlike traditional pseudo relevance they use llm
    - try different prompts
    - it is more powerful than the traditional methods
    - it is similar to Query2Doc, but studies different prompts and different models
    - stating that query expansion wih prf is bad since the retrieved doc do not have to be relevant
    - the chain of thought was a good expansion, otherwise it was really good
    - the query also benefited retrieving top3 results and use it as prf
4. [Query2doc: Query Expansion with Large Language Models](https://arxiv.org/abs/2303.07678) (2023)
    - the method generates pseudo documents by few shot prompting and then expands the query with generated pseudo documents
    - it explains the history of pseudo relevance feedback, rochio, but rm3 has limited results on popular datasets
    - most state of the art dense retrievals do not adopt this technique
    - also doc2query methods are good for sparse retrieval
    - generally it benefits the methods
5. [Query Expansion Using Contextual Clue Sampling with Language Models](https://arxiv.org/abs/2210.07093)   (2020)
   - there was some work on context generation with llm, but they argue that it should balance the diversity (generate multiple context) and relenvance, since one context can lead to query drift
   - but generating multiple context can cause hallucinations
   - they learn the seq2seq model, and generate 100 context using "beam" and then complete cluster them and choose the most probable generated, and then query the external source with multiple context and sort them based on the probability of generation context.

### To read

- [Precise Zero-Shot Dense Retrieval without Relevance Labels](https://arxiv.org/abs/2212.10496)
  - **HyDe**
  - instruct language model to generate hypotetical document based on the query
  - the document captures relevance patterns but is unreal and may contain false details
  - then a an unsupervised contrastively learned encoder encodes the document into an embedding vector
  - the vector identifies a neighborhood in the corpus embedding space, where similar real documens are retrieved based on vector similarity
  - the second step ground the generated document to the actual corpus

- [InPars-v2: Large Language Models as Efficient Dataset Generators for Information Retrieval](https://arxiv.org/abs/2301.01820)

### For reference

  - [A systematic survey of prompting methods in natural language processing](https://dl.acm.org/doi/full/10.1145/3560815)
    - a survey on prompting
- [Take a Step Back: Evoking Reasoning via Abstraction in Large Language Models](https://arxiv.org/abs/2310.06117)
  - **step back prompting**
  - query rewriting with llm
  - evoke reasoning over abstract responses
  - Inspired by the fact that when faced with challenging tasks humans often step back and do abstractions to arrive at high-level concepts and principles to guide the process
  - they propose STEP-BACK PROMPTING to ground reasoning on abstractions to reduce the chance of making errors in the intermediate reasoning steps
    - [Recitation-Augmented Language Models](https://arxiv.org/abs/2210.01296)
      - recite the answer before being prompted
    - [Chain-of-thought prompting elicits reasoning in large language models](https://arxiv.org/abs/2201.11903)
      - elicitation of a step by step why it did what it did
      - there is also approach called **scratchpad**
- [Query Rewriting for Retrieval-Augmented Large Language Models](https://arxiv.org/pdf/2305.14283.pdf)
  - **the RRR princip**
  - it seems that they query the web with the provided query and then they rewrite it
  - also there is a version in which they use reinforcement learning to align the rewriting with the queries.
- [Generation-Augmented Retrieval for Open-Domain Question Answering](https://aclanthology.org/2021.acl-long.316/) (2021)
  - it expands queries with heuristically discovered context
  - eg generate a title for a passage then being easier to retreive it
  - GAR