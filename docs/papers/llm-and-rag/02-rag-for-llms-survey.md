# Retrieval-Augmented Generation for Large Language Models: A Survey
 
- [Link](https://arxiv.org/abs/2312.10997) (last revisited january 2024)

## Intro

LLMs demostrate a good capabilities but face hallucinations, outdated knowledge, non trasparent, untracable reasoning process, especially when queries extend beyond training data.
Rag came into place to incorporate knowledge from external resources.
This enhances credibility of the models.

In this paper, they review of rag paradigms.
In general, before querying llm, there is additional step to query external resources and augment the llm query with the retrieved resources.

Formerly in 2017 wih emerging transfoermer architecture, the primary thrust was on assimilating additional knowledge thourgh pretraining models to augment language models - optimizing pretraining.
Thenm a concentration on inference with minority dedicated to fine tuning.
Then as llms progressed, the hybrid approach, combining strength of rag and fine tuning was done.

In this paper, they want to summarize and organize rag approaches.

## Definitions

Technologically, rag has been enriched thourgh various innovative approaches - what to retrieve, when to retrieve, how to use the retrieved information.

- what to retrieve
  - has processed from simple token and entity retrieval to complex structures like chunks and knowledge graph
  - retrieving structured text provides more information while sacrificing efficiency
- when to retrieve
  - from single, to adaptive and multiple retrieval methods
  - high retrieval frequency brings more info but less efficiency
- how to use
  - to model architecture - input, intermediate and output layers
  - although the intermediate and output layers are more effective, there are problesm with the need for training.

RAG paradigm employs a synergic approach with ir and in context leaning to bolster llm performance.
In rag there is no need for retraining.
It become famous.
It works in three steps:
1. corpus is partitioned into discrete chunks, upon which vector indices are constructed utilizing an encoder model
2. rag identifies and retrieves chunks based on their vector similarity to the query and indexed chunks
3. the model synthetizes a response conditioned on the contextual information

- There are also three cathegories
  - naive rag
  - advanced rag
  - modular rag

## Naive rag

Traditional process - indexing, retrieval and generation.

- Indexing
  - lexicalization, cleaning...
  - the text is segmented into smaller more managable chunks
- retrieval
  - vector sim search
- generation
  - synthetize retrieved infor into the prompt
  
- drawbacks
  - retrieval - low precision, misaligned chunks leading to hallucinatoins or mid air drop, low recal, outdated information also causes problems
  - generation - hallucinations since the model disregards the prompts and the info
  - augmentation - how to effectively intergrate the retrieved things
  - importance of passage is not clear
  - the problem that llms depend on the retrieved info and just reiterate it

## Advanced rag

To tackle the previoius problems.
It introduces pre retrieval strategies and post retrieval strategies.
Also introduces indexing approaches such as sliding windows, fine grained segmentation and metadata.

- Pre retrieval
  - data granularity
    - standardization of text, consistency, factual accuracy, rich context to imporove rag, dispelling ambiguity in entities and terms
  - optimizing index - better chunk size, querying multiple paths
  - metadata - referenced metadata, such as dates and purposes
  - aligmens - issues and disparities between documents - adding hypothetical questions to rectify aligment issues
- Retrieval 
  - potentially fine tuning embedding, especially for professional domains dealing with evolving or rare terms
    - baii 
      - fine tuning to optimize retrieval relevance, the data can be generated using language models to formulate questions grounded on document chunks which are then used as fine tuning pairs
  - dynamic embeddings adapts to the context in which words are used, which uses single vector for each word (like bert models)
- post retrieval
  - the prompt is limited
  - re-ranking 
    - to retrieve the most relevant content to the edges of the prompt
    - diversityranker 0 prioritizes reordering based on document diversity
    - lost in the middle ranker 0 alternates placing the best document at the beginning and end of the context window
    - recalculating semantic similarity between relevant text and the query
  - prompt compression
    - noise affects performance
    - selective context - utilizes small language models to calculate prompt mutual information

## Modular rag

Modularized approached, it enables serialized pipelline or end to end traning approach across mutliple modules.

### New modules

- search modules
- memory module
  - capability of llm - the most similar to the current input
  - there is a retrieval enhanced generator to create unbounded memory pool iteratively combing original question and dual question, by employing a retrival enhaned generative model that uses its own output to improve itself, the text becomes more aligned with the data distribution during reasoning process, the model own outputs are utilized instead of the training data
- fusion
  - multi query approach that expands user queries into multiple
  - parallel vector searches of both the original and expanded queries and intelligent reranking
- routing 
  - different resources based on situation
- predict
  - problem with redundancy and noise
  - instead of directly retrieving data from a source, this module utilizes llm to generate necessary context
  - the content produced by llm is more likely to contain good information

## Retrieval

How to create a good retriever?
What methods can align semantic spaces of queries and docuemnts?
How can the retrievers output be aligned with preferences of the llm?


### Enhancing semantic representations 

Two methods for building accurate semantic spaces.

- chunking strategy
  - need to know the best chunking strategy
  - based on model - sentence bert a good with single sentence, while gps better with blocks of 512 tokens
- fine tuning embedding models
  - the embedding effectiveness is crucial
  - promiment embedding models such as angle, voyage, bge
  - but their problem is limited when facing specialized domains
  - two paradigms
    - domain knowledge fine tuning
      - to ensure that model captures domain specific information
      - crutial is to utilize domain specific datasets for fine tuning
      - llama index introcudec suite of pivotal classes and function to enhance embedding models
      - dataset - query, corpus and relevant documents
    - finetuning on downstream tasks
      - finetuning embedding models by harnessing capabilities of llms
      - the llm as a few shot query generator (PromptAgator) to create task specific retriever, addresing challnges in data scarse domains
      - (llm embedder) exploits llms to generate reward signals for data across multiple downstream tasks
  - this methods improve semantic repre but may neot be optimal compatibility with certain llms

### Aligning queries and documents

The original query may suffer from imprecise phrasing and lack of semnatic information.
There is the need to align semantic space of queries and documents.

- Query rewriting 
  - Query2Doc or Iter-retgen
    - laverages llms to create pseudo documents by comning the original query with additional guidance
  - HyDE
    - constructs query vectors using textual cues to generate a hypotetical document comparing essential patterns
  - rrr
    - introduces framing that reversed the traditional retrieval and read order focusing on query rewriting
  - step backprompting
    -  eneables llms to perform abstract resoning and retrieval based on high level concepts
  - multi query retrieval
    - generate multiple queries and query
- Embedding transformation
  - beyond query rewriting there is more granular techniques
  - llamaindex introduces an adapter module that an be integrated following the query encoder, which faciliates finetuning, and placing the query into a latent space that is more closely aligned with intended tasks

### Aligning retriever and llm

In retrieval pipeline, doing betterment in retrieval might not get us better results with llm.
This section includes 2 methods to align retrieval hit outputs with the preferences of the llm.

- Fine tuning retrievers
  - several studies utilize feedback signals from llm to refine retrieval models
  - AAR 
    - supervisory signals for pretrained retriever using encoder-decoder architecture, they identify lms prefered documents thourgh fid cross attention scores.
    - then the retriever does fine tuning
    - there is suggested that llms may have preference for readability rather than rich information documents
  - REPLUG
  - UPRISE
    - treating llm as labeler and supervisor of retriever
- adapters
  - finetuning can be difficult from limited computational resources

## Generation

### Post retrieval with frozen llm

In the realm of untunable llms, many studies rely on well established models.
There are challenges including limitations on context length and susceptibility to redundant information.
Post retrieval processing involves treating, filtering or optimizing the relevant information retrieved by the retriever.
The methods usually are compression and reranking.

- compression
  - from the retrieved data, pick the most notable information
- reranking
  - reranking retrieved documents that are pushed to the llm
  - llms declines when additional context is introduced
  - this solves context window expansion during retreival but enhances retrival efficiency and responsiveness

### Finetuning llm for rag

- general optimization process
  - traning data consists of input-output pairs
  - there are methods with joint encoder and dual encoder
    - joint encoder
      - encoder-decoder
      - encoder converts the input and decoder combines the encoded results to generate tokens in an autoregressive manner
    - dual encoder
      - two independent encoders
      - they encode input query,context and document
      - then it goes through bidirectional cross attention processing by decoder
- contrastive learning
  - training data contains intections pairs of input and output
  - since traditional methods can lead to exposure bias

## Augmentation in RAG

Three aspects - augmentation stage, sources of augmentation  data and augmentation process.

### Augmentation stages

- Pretraining  stage
  - methods to bolster ptm for open domain qa through retrieval based strategies
  - REALM
    - adopts knowledge embedding and frames training/tuning as retrieve then predict workflow
  - RETRO
    - large scale pretraining from scratch
  - atlas
    - retrieval mechanism into t5 architecture
  - COG
- Fine tuning stage
  - finetuning retriever
    - get high quality semantic information
    - align retriver with preference of llms
  - finetuning generator
    - better outputs
- Inference stage

### Augmentation source

- Unstructured data
  - text, phareses, tokens
- Structured data
  - kgs
  - RET-LLM
    - constructus kg memory from past dialoguies for future reference
  - sugre
    - employs gnn to encode relevant kg subgraphs
- llm generated data

## Augmentation process

Problems with the lost in the middle - when a sigle retrieval yelds reduntant content that may dilute or contradict essential information.
Single step is not sufficient for complex problems.

There are - iterative, recursive, and adaptive retrievals.
- iterative
  - model engages in cycles
  - enhancing depth and information retrieved
- recursive
  - results of one retrieval are used for the results of the another
- adaptive
  - dynamic adjustments

## Final thoughts 

The paper continues, but delves deeper into evaluation, which is not needed for me.
In general I dont think I will be training the llm itself.
But the insids of the retrival parts were beneficial.

- Mainly
  - the naive rag in question what is the best thing to ask and ask for reranking
  - retrieval strategies
    - pre retrival
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
    - some llms prefer different outputs
    - most of the things need a lot of data

- intereting papers
  - [PromptGator](https://arxiv.org/abs/2209.11755) for specific retrievers with not enough data
    - the idea is that for a given task comes with a short description and a few examples
    - they propose prompt base query generation for retriever, which leverages llm as a few shot query generator and create task specific retrievers based on the generated data
    - they say that it is hard to make nn perform well based on few data
    - this paper explains the problems with datasets
    - the promptgator creates task specific prompting, which in tur enables generating a large set of synthetic queries for trianing retrievers
    - they want to show that llm can be used to generate efficient end to end retriever with high accuracy
    - the key idea of PROMPTAGATOR is to transform the few examples into many more examples by prompting a LLM, instead of using them to train a retriever directly
  - [KnowledgeGPT](https://arxiv.org/abs/2308.11761)
    - the idea is that they use gpt to create for accessing and creating knowledge base
    - the upon query the llm will generate code which will extract entities based on the query and retrieve them
    - then the retrieved things are inputed into the llm
    - but how do they do the entity linking???
      - they even work with aliases
      - they asked the gpt to create the code
    - but i could not decipher how the entity linking is done