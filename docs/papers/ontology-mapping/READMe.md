# Ontology mapping

The idea here would be if user writes text, there could be a tool how to match it to the concepts in the ontology.
The problem here is that the text itself can be a keyword and lacks edges to other concepts, hence it would be difficult to deduce context.

I found a paper on llm matching which works in multiple ways as a RAG.
It firstly finds candidates based on embddings of lexicalized classes and properties.
And then they ask llm if the candidates are similar to the given entity.

### To read maybe

- [Knowledge graph embedding methods for entity alignment: experimental review](https://link.springer.com/article/10.1007/s10618-023-00941-9)
  - bert_int method is the best

- [Background knowledge in ontology matching](https://www.semantic-web-journal.net/content/background-knowledge-ontology-matching-survey-0) (2022)
  - good matchers are using BERT models just LLM
  - KGMatcher from google is good or WiktionaryMAtcher 

### For reference

- [OLaLa: Ontology Matching with Large Language Models](https://arxiv.org/abs/2311.03837) (2023)
  - they create embeddings for all classes in the ontology via sentence bert and lexicalization of properties
  - then they find candidates with sentence bert
  - then they ask large language model whether the text are the same
  - and they look for response in the model prompt