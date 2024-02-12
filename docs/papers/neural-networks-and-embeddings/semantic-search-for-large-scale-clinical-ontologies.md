# Semantic Search for Large Scale Clinical Ontologies

[Link](https://arxiv.org/abs/2201.00118)

### Intro   

Finding concepts in large ontologies can be challenging when queries use different vocabularies.
A search algorithm that overcomes this problem in situations where concepts can be referred to in different ways.
They use deep learning based approach to build search system.
They propose Triple-BERT and a meethod that generates training data directly from ontologies.

There exists a large ontology SNOMED CT but it is difficult with adoption:
1. much of the data is free text and needs to be mapped to a standart ontology
    - using NLP, free text is analysed to identify relevant concepts
    - identify spans of text that represent relevant concepts (information extraction)
    - and mapping these concepts to concepts in chosen ontology (information normalisation)
2. existing systems use their own code systems and it is not feasible to replace them with SNOMED CT.
   - mapping between ontologies
   - ontology matching 

Solutions exists for both problems but are very specific.
They propose general solution, in which they use short spans of text as input.
They make a new algorithm based on learning derived word representations for finding good concepts even in absence of common vocabulary.
Input is free text (normalisation), concept in the second case.

### Related Work

- models to overcome vocabulary mismatch problem
  - Word2Vec, GloVe, fastText
    - words that are used and occur in the same contexts tend to purport similar meanings
    - once trained every word is encoded by a vector, but it is static - vector is same regardles  of context of use
    - those vectors can be used as inputs to combination function, or another nn model to derive embedding vector of a query or document
- contextualised word embeddings - deep long short-term memory
  - CoVe, ELMO, FLAIR
  - dynamic embeddings based on contexts
- transformers 
  - BERT, XLNet, RoBERTa
  - state of the art nlp tasks
  - a key idea in these methods is that the meaning of a word in a sequence is represented by how much attention of that word attracts the other words in the sequence
  - once training is done, they output all tokenized words of a given sentence
  - then those vectors can be combined in different strategies to derive a semantic embedding vector of an input sequence
- Search engine
  - a special feature is that the to-be-searched docs are concept labels, which are short and therefore sentence embedding methods are higly relevant
  - because they compute semantic relatedness between this type of label.
  - Doc2Vec, Skip-Thourgh, InferSent, Universal Sentence Encodet, Sentence-BERT
  - Doc2Vec is extension of Word2Vec trained with large unlabelled data
  - Skip-Thourgh is extension of Doc2Vec
  - USE trains network which augments unsepervised leaning
  - InferStern trains Siamese BiLSTM network with a max pooling layer on top.
  - Sentence-BERT is better then InferStern
  - these models have been trained on nl inference data sets, input to a model is a pair of sentences and output is an inferred relation between them

### Method

They use a method similar to Sentence-BERT - Siamese architecture, classification and regression objective functions, but instead they use Tripled network, which processes three inputs in parallel and a triplet loss function, which is a learning to rank metric for three inputs.

The main idea is to transform every concept label into appropriate embedding vectors in a vector space, so their locations preserve sematic relations between concepts in an ontology - concepts that are synonyms should be close.
But on the other hand, by applying distance calculation on the tree structure - distance between two concepts is computed by the sum of distances from those concepts to their lowest common ancestor.
Therefore we want distance to a parent be closer than distance to a sibling.
That must work for synonyms too.

### Label embedding with Triplet-BERT

Triplet-BERT was traine to produce a semantic embedding vector for a short text spans such as concepts' labels or user queries.
It is a Triplet-Network - three instances of the same embedding layer containing a shared BERT network and a pooling layer.
Requires three text inputs:
  1.  anchor input  
      - in this work, it is a user query (maybe synonym?)
  2.  positive input
      - a high relevant concept (the concept label) 
  3.  negative input 
      - a less relevant concept to the query (maybe sibling of a parent)

The objective is that the anchor input is closer to the embeddding vector of the positive input that to the embedding of the negative input.
Each input is fed into the bert to produce a list of intermediate embedding vectors, then a pooling layer combines these vectors to produce a summary vector for the input.
After that we get three vectors for each input, we compute disances, and objective function conpares the two distances and indicates whether the model needs to adjust its parameters.
Once training is completed, the embedding layer is used to produce embedding vectors for any user text query as well as concept labels in the ontology.
After that, the consine similarity is used between the concept labels and user queries.

### Training data

The NN need a lot of training data.
There exists datasets where each entry consists of a pair of sentences and a label that is either a relationship type or a semantic similarity score.
These entries cannot be used in this work.
They propose a method to generate the data for training based on distances in the ontology hierarchy.
4 mills of entries from SNOMED CT.
Algorithm is straight forward in the paper page 4.

Otherwise it is good.


It has complementary paper [Self-learning ontological concept representation for searching and matching](https://www.semanticscholar.org/paper/Self-learning-ontological-concept-representation-Ngo-Koopman/6985beaffc63602f8978e0c58cf7855c089adc9c)