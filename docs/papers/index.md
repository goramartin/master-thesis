# Papers index

The file contains a brief description of folder strucures.
Apart from that, it also contains not classified papers or topics which I deemed not necassary to read but include it for future reference if needed.

Folders:
1. searching-ontologies
   - folder contains papers on finding ontologies on the web
   - mostly there are frameworks for ranking ontologies based on certain criteria
   - i looked into it because usually the few initial steps in the solutions include finding concepts in the ontology, or in general views on tologies and ranking
2. class-importance
   - folder contains papers on importance of classes in ontologies - the question what classes are important in the ontology
   - it is somewhat continuation of my research from the first folder
   - also it contains an important RAG
3. entity-linking
   - folder contains papers on entity linking to wikidata entities in text
   - the idea was that the query could contain entities that could be linked to the wikidata entities directly
4. necasky
   - folder contains papers provided by necasky
5. ontology-mapping
   - folder contains papers on ontology mapping and aligment
   - the idea was to see the query as a concept and then create embeddings or ask llm (which i exactly found)
6. neural-networks-and-embeddings
   - reranking and combining results  
   - retrieval
     -  folder contains papers on neural networks regarding embeddings, including concept similarity, using knowledge enhanced transformers, exploration of entity retrieval, joint embeddings and graph embeddings
7. rag and query expansion
   - folder constains papers regarding llms and retrieval augmented generation
   - from the llms it contains mostly query expansions using llms and ways of prompting
   - from rag it contains a summary of a survey

## Topics and papers not classified yet

### Termpicker

Stealing the written report from Krystof.

[Link](https://github.com/georgeus19/MastersThesis/blob/main/docs/papers/term-picker.md)

### Keyword search over Knowledge graphs

This sounds like something very close to my topic, but the resulting operation is somewhat returning the subgraph containing all the keywords.
It seems that the first phase is to locate all the keywords matching and then building some sort of Steiner-Tree problem for constructing the minimal subgraph. 

- surveys
  - this one is the most important [A systematic literature review and classification of approaches for keyword search over graph-shaped data](https://www.semantic-web-journal.net/content/systematic-literature-review-and-classification-approaches-keyword-search-over-graph-shaped) (2023)



