# 8. meeting

1. Overview of what I did

## Overview of what I did

### Changing containerization

- Changing containeinerization of the Research project and Diploma
  - Previously:
    - Containers needed to by run separately.
    - A lot of manual labour even for development.
  - Now 
    - Docker compose starts all the necessary parts start.
    - Only the Ontology API service is visible from the outside.
    - The rest of the services are connected via docker bridge and are not accessible from the outside.
      - No need to set up security.

<br>

- Ontology API service
  - Contains a secure route for restarting the service -> load new ontology.
- Preprocessing
  - Now can be run in docker.
  - Connects to the internal docker bridge network and can access other service.
    - E.g. instruct Ontology API service to reload.

### Preprocessing for the new search engine

- Lexicalization of classes/properties
- Dense embeddings
- Sparse Learned Embeddings
  - Using the newest and most performant splade model.
  - But need access via token.
- Problem with paralelization.
  - Need to rerun it sequentially.

### Search engine containers (c4)

- Python API service
- Dense Embedding service
- Sparse Embedding service
- Cross-encoder reranker service

<br>

- Elastic Search
- Qdrant

### Research of reranking

- Missed theory for reranking
- Found theory on the methods I want to do.
- Methods are still the same, but now we have background.





