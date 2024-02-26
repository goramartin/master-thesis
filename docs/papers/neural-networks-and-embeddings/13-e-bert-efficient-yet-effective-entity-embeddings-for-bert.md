# E-BERT: Efficient-Yet-Effective Entity Embeddings for BERT 

[Link](https://arxiv.org/abs/1911.03681)

I did not read it all, just to get the general idea of the method.

## Intro

A new way of injecting factual knowledge about entities into pretrained BERT.
They align Wikipedia2Vec entity vectors with bert's native wordpiece vector space and use the aligned entity vectors as if they were wordpiece vectors.
It requires no expensive further pretraining of BERT encoder.
The bert encoder is unchanged.

Previously KnowBert and Ernie based on principle that bert is adapted to entity vectors.
They introduce new layers to feed pretrained entity vectors into the transfomer and need additional pretraining.

E-bert works with idea that entity vectors be adapted to bert.
Wikipedia2vec embeds words and entities into common space.
Given vocabulary of words and vocabylary of entities, it learns a look up embedding function.
Its loss has three parts: word2vec on vocabylary of words, graph loss operating on wiki hyperlinks, anda version of word2vec where words are predicted from entities.
Loss (3) ensures entiteis and words are embedded into the same space.

## Method

They want to transform the vectors of entity vector space from wikipedia2vec to make them look like bert vectors.
They model the trasnformation as an unconstrained linear mapping. 
Ther bert wordpiece does not contain eneitties, they fir the mapping on bert wordpieces and wiki words vocabulary.

After alignment the enetity vectors should be fed into the bert.
1. concat
   - e bert combines entity ids and wrodpieces by string concatenation with the lash symbol operator
   - the entity id is embedded by e bert and the rest is by bert
   - after the embedding operation
   - the sequence of vectors is combined with position and segment embeddings and fed into bert just like normal sequence of wordpiece vectors
   - this is similar to ernie and knowbert
2. replace
   - substitute entity surface form with entity vector.  

