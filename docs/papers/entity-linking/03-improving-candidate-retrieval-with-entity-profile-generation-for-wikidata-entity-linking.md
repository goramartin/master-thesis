# Improving Candidate Retrieval with Entity Profile Generation for Wikidata Entity Linking
 
[Link](https://arxiv.org/abs/2202.13404) (2022)

## Intro

To narrow down the search space, they propose novel candidate retrieval paradigm based on entity profiling.
Wikidata entities are first indexed into a text seach engine.
During inference, given a mention and its context, we use a sequence to sequence model to generate the profile of the target entity - which consists of its title and description.
They use the profile to query the indexed search engine to retrieve candidate entities.
Their approach complements the traditional approach of using wikipedia anchor text dictionary, enabling them to further design a highly effective hybrid method for candidate retrieval.
Combined with a simple cross attention ranker, their complete EL framework achieves state of the art results.

- But how do they find the mentions?

## Methods

**They assume that the mentions in the text are given. Identified by some extraction module.**

It consists of two modules: candidate retrieval and reranking.
The candidate retrieval is combination of dictionary based approach and profile based approach.
The reranking is done using simple transformer based cross attention reranker.


### Candidate retrieval

Dictionary approach - idea is to estimate mention to entity prior probabilirty.
Prior estimation - the anchor texts in wikipedia are frequently used for estimating prior probability.
Wikipedia apporach is not applicable.

They propose a new method.
They index entities into elastic search.
During inference, given an entity mention, and its context, they use seq2seq model to generate profile of the target entity.
Then they use the mention and the new profile for formulating the query.

How to generate the profiles?
A straight forward approach to query ES is to directly use the literal string of the input mention.
But it is not enough.
A well trained generation model can generate a description that closely resembles the target entity actual description.
**But that would imply that we need a context.**

They train a conditional generation model for generating the profile of the target entity, where the condition is the mention and its context.
The generation process models the conditional probability of selecting a new token given the previous tokens and the input to the encoder.

In the elastic search, they try to score each entity based on 3 criteria:
1. similarity based on mention and title + alias
2. the same for generated title
3. sim. between description field and the generated

### Hybrid approach

They want to combine wikidata approach with dictionary.
Since every wikipedia article can be mapped to wikidata.
The combine the lists produced by these two methods.
And then they use the candidate gradient boosted tree model to assign a score to every candidate.
Then it is sorted.

For features they combine:
1. string based features: levensthein ratios, jaro-wrinkler distance, number of common words between mentions surface forn and the candidate entity's name and aliases.
2. number of common words between the mentions context and the entity name and aliases.
3. Number of common words between the mentions surface form and context and the entity description and category
4. they also use features that indicate the initial rankings of a candidate entity

### Cross attention reranker

They model the raranking problem as a binary classification problem and fine tune a basic transofrmer based reranker for the task.

Input of reranker is concat. of the mention repre. and the candidate entity repre.

## Experiments

- Target knowledge base
  - wikidata dump
  - they exclude items that correspond to wikimedia internal administrative entities
  - they include only some entities in the end
- Training 
  - they use wikipedia anchor texts and their corresponding wikidata entities as the supervision signals
  - we create a training set of 6 milion paragraphs and a validation set of 1000 paragraphs
  - they dont do fine tuning

## Evaluation

It has good performance.
The hybrid method works.
They compared it with genre and blink (facebook entity linking things).
The dataset they created is missing, and in general it was trained on wikipedia dataset with linkage to wikidata.
All in all, it focuses only on disambiguation phase and not how to find the mentions in the text.
There exists docker image with the entity linking framework, but the code is not open and the dataset is not present.
Also it specifically assumes there is some context to the query.

