# KEPLER: A Unified Model for Knowledge Embedding and Pre-trained Language Representation 

[Link](https://arxiv.org/abs/1911.06136) (2020)

I did not read it all, just to get the general idea of the method.

## Intro

Pretrained language models well capture text knowledge and knowledge embeddings well capture structure.
How to take advantage of it together?
It integrates factual knowledge into plms but produce effective text enhanced ke with strong plms.
They encode textual entity descriptions with plm as their embeddings, and then jointly optimize the ke and lm objectives of ke and mlm.
They encode text and entities into the unified space with the same plm encoder.
For ke the objective, they encode entity descriptions and then train them with the conventional methods for ke.
For the mlm they use existing approach.

Previous works learn embeddings from different ke model and cannot be easily aligned with language model.
They require entity linked to link text to corresponding entities, making htem suffer from error propagation problem.
They also use additional inference overhead when linking.

KEPLER is able to perform ke in the inductive setting - it can produce embeddings for unseen entities from their descriptions.
While other methods are inherently transductive and they can only learn representations for shown entities during training.

## Method

KEPLER implicitly incorporates factual knowledge into language representations by jointly training with two objectives.

For text encoder they use BERT.
The encoder needs tokenizer to convert pain texts into tokens - htey use roberta tokenizer.
They do not modify transformert encoder.

To integrate factual knowledge into kepler, they adtop ke objective.
Each entity and relation is assigned a vector in the same space.
They encode entities into vectors by using their descriptions.
1. name with a description for entities and name for relation
2. name with a description for entities and name with a description for relation
3. name with a description with relation description in one
For the loss they use loss from TransE

For MLM is objective from bert and roberta.
MLM during pretraining selects some of the input positions and predict tokens at these position within fixed dictionary.
They use roberta model but use the objective to tackle the forgetting.

The best results are on kepler with embedding from wikidata.

## Comments

This seems like the closest thing i could get with the pretrained language models with knowledge enhance.
It works with wikidata, and possibly could be usefull with the code as well (if there is some).