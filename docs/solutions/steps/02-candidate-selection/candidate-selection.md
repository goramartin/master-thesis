# Candidate selection

- main topics
  - full text search
  - vector search
  - subclassing with properties
  - topic modeling

## Full text search

- For this I would use ElasticSearch and its native BM25 ranking function.
- Also there is an option with the BM25F as combined fields
  - but that requires to set a parameter that minimum should match in %
- I looked into other databases (viz. view databases overview) but it seemed that elastic is the best.
- I know it the best

- There could be search based on multiple options
  - label and aliases (as is done now)
  - label, aliases and description
  - label, aliases, description and additional information  
    - has cause, has effect, parts, part of, has characteristics, has use

- basically a document retrieval
- So have decided to use elastic search:
  - the problem is that the previous query might not be that good
  - so i was thinking that maybe creating additional fields tht contains merged things.
  - One for english text, one for standart tokenizer, and one for keywords
  - the keywords should be present only in separate fields
  - additionaly - description could be concatenation of all of the things together not just the ones.

## Vector search

- dense vs sparse (elser, spladev2, colbert)

- For this I would do lexicalization of the data.
  - labels, aliases, description and subclass information
  - additional fields lexicalized
    - top properties
    - characteristics
- That depends on the context view of the lm
- After that there is creating an embeddings for the texts.

- dont forget 
  - ann
  - exact nn
  - hdsn and other methods to index the data
  - picking the embeddings based on our previous research
  - hybrid search
  - benchmarks
    - mteb, beir - they have public results

### Lexicalization

- Needs to count for tokens, models have a limit
- Repeat the label for each sentence since it improves results.

### What dense embeddings 

- sentence transformers
  - symetrics
    - good for sentence similarity and capturing meaning
  - assymetrics
    - question and answer types

- I looked into MTEB and found a good models
- Also there is the beir benchmark

- over all 
  - sentence transformers - the best model or all mini
  - the one from mxbread
    - fairly new one, nice documentation and small size 0.44 and 1024 size
    - they did not train it on the testing data
  - baii bge large en
    - but probably good for assymetric
    - faily used one
    - 1.34
  - uae large v1
    - 1.34
    - but probably good for assymetrics
  - gte large
    - 1.34

### What sparse encoders

- There is the elser from elastic search
- there is the general spladev2, which the elser is based on
- [sparse](https://qdrant.tech/articles/sparse-vectors/)
  - there are links to other stuff like papers why it was good

### Hybrid search

- based on qadrant and elastic search
- needs fusion

## Subclassing 

- either use all the properties for each class
  - i have tried this, but the overall number of properties was huge
  - the final file was just 19GB
  - if did not fit the web server we have

- or use the other way around with setting parents
  - for each class compute the parents in the hierarchy
  - but we know that only limited number of parents contain some number of property definitions
  - so we will mark only parents that do contain some properties
  - further we can do reduction
    - instead of keeping the properties as they are
    - we will traverse the hierarchy and remove the properties that are the same in parents
    - eventually properties on entity (41 properties) will be only on the entity class
    - this way the properties will not have duplicities in the children hierarchy

- sparse vectors for the properties
  - difficult to combine it with search and usage as filter

## Topic modeling

- how to further narrow down the search results
- based on the statistics many classes contain similar descriptions and labels
- the search can be ambigious

- lets create topis
  - user will choose
  - or it will be implicit

- both solution are hindered by what topics should be used
  1. topic2bert and bertopic
     - nice solutions but depend on the text and can be difficult to explain why it is that way, would work only in implicit way
  2. choosing some topics
     - difficult to model - what belongs inside?
     - there are few options
       - wikipedia topics
         - better
         - there is an upper level of topics
         - the most general ones
         - difficult to access programatically
           - messy, slow apis, difficult to locate
       - wikimedia topics
         - difficult to access
         - mostly to describe projects of wikimedia   

- but how to assign them in case of wikipedia?
  - based on instances by iterating the topic hierarchy of wikipedia
    - but we have slow api
    - downloading the dump? cannot get into the format
  - based on instances by using embeddings of the instances
    - slow 108_000_000 embeddings is diffucult
  - based on classes by assigning them to the topics by embeddings
    - simpler and straightforwards
    - how many topics to assign?
    - should we use hierarchy?