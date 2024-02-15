# Wembedder: Wikidata entity embedding web service

[Link](https://arxiv.org/abs/1710.04099)

## Intro

A web service for querying an embedding of entities.
Trained on dump using Gensim's Word2Vec and a simple graph walk.

The aim is to return a similar entities based on a query and some multilingual properties.

## Method

They use Gensim Word2Vec on preprocessed wikidata dump.
From the dump, they create triples in the following way:
1. Extract rdf triples that represent "subject" and "object" as items.
2. these triples form a sentence
3. the sentences are input to the word2vec 
The model parameters are included in the thing.

The query aims to return the most similar entities.
Also it is able to compare them in terms of similarity.

## Conclusion

It is interesting idea, but it only relys on the item to item things.
Maybe I could represent the entities in the same way, but create different sentences.
The problem is it would exclude the sentences that occur only few times.