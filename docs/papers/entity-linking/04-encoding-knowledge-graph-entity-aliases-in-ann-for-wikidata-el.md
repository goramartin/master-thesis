# Encoding Knowledge Graph Entity Aliases in Attentive Neural Network for Wikidata Entity Linking (septempber 2020)

[Link](https://arxiv.org/abs/1912.06214)


## Intro

Wikidata as the core background KG along with its inherent challenges, has not been studied particularly for the task of EL.
They analyze impact of additional conctext from Wikidata on attentive neural networks for solving its entity lining challenges.
They propose arjun to recognise entitites from text and link them to equivalences from wikidata.
In the first step, arjun uses deep attentive nn to identify surface forms of entities with the text.
It uses local kg to expand each surface form from previoius step to a list of potential wikidata entity candidates.
Then it is fed into second ann to disambiguate the wikidata entities furher.
The release source code apparently.

## Related work

Using KG as background info is recent.
Falcon for linking of questions - for dbpedia some from wikidata..
They reuse it and expand with all entities present in the wikidata.
A neural network approch, the paper in reference, but assumes entities are recognized.
Input to their model is a sentence one wrong wikidata qid and one correct quid - using attention based model they predict correct qui in the sentence - it is a classification problem.
Their model is not adaptable for enn to end input due to restrictoin.

## Method

They first need to to surface form extraction - recognize surface forms of entities in the text.
It is similar to NER, it disregards the type of entities.
The second one is entity disambiguation - mapping each surface form into a set of te most probable entities from kg.

1. deep attentive neural network to identify the surface forms of entities
2. local kg to expand each surface form to a list of potential wikidata entity candidates
3. surface forms coupled with potential candidates are fed into the second attentive neural network to disambiguate the wikidata entities further

They device context-aware approac based on attentive nn for 1 and 2.

- Local KG
  - relies on wikidata as background kg
  - its unique characteristics can be used - aliases
  - they extracted entities with english labels and aliases
  - they use aliases and aliases
  - and large portion is reused from local kg build by [18]
- Model architecture
  - for the task 1 and 3 the task is inspired by [15]
  - concists of an encoder, decoder, and attention layer.
  - they dont claim that extension of the [15] is novelty.
  - they experiment with estabilished concepts of lstm.
  - they extend [15] with bidirectional lstm model for encoder and one directional lstm model for the decoder.
    - the input of encoder is source text
      - encoder encodes the complete sequence and te decoder unfolds this sequence into a targer sequence
      - each target sentence ends with EOS
      - each word from source is projected to its vector repre acquired from embedding model R^d, the transformation is represented in the matrix X = [x1, .. xN], xn is vecotr of size d for word in te sentence 
    - the lstm layer    
      - The LSTM Layer: In our model, the encoder and the decoder consist of single layer of Bi-LSTM and LSTM respectively
    - attention and decoder layer
      - decoder takes SOS token vector and the encoder final states as initial inputs to start decoding source text sequence into target sequence
  - entity mapping
    - local kg acts as a source of knowledge
    - it is an indexed graph like in [18] where each entity label is extended with its aliases from wikidata
    - output of task 1 identifies surface forms in the input sequence and mapping retrieves all entities for which entity labels in the local kg matches with the surface form
    - next the list of candidates is passed to the step 3

## Set up

There is T-rex available dataset used of anotated sentences from wikipedia to wikidata entities.
They say why other datasets are bad.

They implemented the approach using pytorch and elastic search.
The semantic search returns entity candidates with a score.
They reuse implementation of falcon local KG for the same.
The reused pre-trained embeddings from hlove for attention neural network.
They employ 300d glove word vectors for the trianing and testing of arjun.

## Evaluations

Not bad.
But there could be used better approaches.
Maybe a better semantic search to find candidates.
The code is missing data also directions how to run the code.
Seems that only falcon 2 is somewhat to use.