# Query Expansion by Prompting Large Language Models

- [Link](https://arxiv.org/abs/2305.03653) (2023)

## Intro

Traditional query expansions are based on pseudo relevance, and uses those documents to extract new query terms.
They assume that the top retrieved documents are relevant to the query.

In this paper they investigate ways to prompt an llm and have it generate a variety of alternative and new terms from the original query.

## Related Work

Query expansion helps retrieval systems by expanding query terms into new terms that express the same concept or information need, increasing the likelihood of a lexical match with documents in the corpus.

Previous attempts used lexical knowledge bases or pseudo relevance feedback.
PRF are useful because they do not need to construct a domain specific knowledge.

There is also ortogonal document expansion which expands documents during indexing.

Also there were attempts to use query expansion with training or finetuning.

In this workd they use llm without training.

This work is similar to Query2Doc.
The difference is that in this work they focus on styding of prompts while q2d single few shot.
In this work they also focus on generating query terms instead of entire pseudo documents.
They also perform study on different llm and only open source models.

## Methods

They insert query with prompt and repeat the query 5 times to upvote the relevance.
They use prompts listed -> take a look page 2.
They combine zero shot, few shot, and prf.

They use flan models.

## Evaluation

Query2Doc is good.
Best performance is obtain CoT.
PRF to the promp helps a lot.
Q2D needs at least 11b parameters to be bettern than prf.
CoT prompts need only 3b parameters to perform nicely.