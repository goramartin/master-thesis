# 1. Meeting

This meeting we discussed the overall solution ideas.

## Necasky comments

Necasky mentioned, that using all the solution would be to much.
He advised me to choose a portion of the solutions.
The solutions could be combined into a simple pipeline so that certain steps could be exchanged with different algorithms.

## My comments

Based on the Necasky comments, I decided I would like to create a small pipeline.
The main steps would be:
1. query expansion
2. retrieving candidates
3. filtering based on properties
4. first phase reranking
5. second phase reranking

From the solutions I would like to implement:
- Query expansion using LLM or Elser from elastic search
- Retrieving candidates using full text search
- Retrieving candidates using vector search
- Reranking based on the wikidata native search
- Reranking based on property usage
- Reranking using LLMs with RAG

There is also an option of trying to learn embeddings via triplebert and bai models.

## To the next meeting

1. Thing about general pipeline and solution selection.
2. I wanted to check the learning embeddings and knowledge enhanced lm.
3. Create a summary on my comments from searching ontologies and class importance.
4. Think about solutions based on the property selection filtering.
5. Check databases and create an overview.