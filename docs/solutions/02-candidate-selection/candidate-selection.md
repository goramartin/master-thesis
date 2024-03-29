# Candidate selection

- main topics
  - full text search
  - vector search
  - subclassing with properties


## Full text search

- For this I would use ElasticSearch and its native BM25 ranking function.
- Also there is an option with the BM25F as combined fields
  - but that requires to set a parameter that minimum should match in %
- I looked into other databases (viz. view databases overview)
- I know it the best

- There could be search based on multiple options
  - label and aliases (as is done now)
  - label, aliases and description
  - label, aliases, description and additional information

- basically a document retrieval


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
- there is colbert

## Subclassing 

- either use all the properties for each class
- or use the other way around with setting parents