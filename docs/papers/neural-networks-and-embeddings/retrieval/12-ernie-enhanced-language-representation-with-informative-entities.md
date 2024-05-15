# ERNIE: Enhanced Language Representation with Informative Entities

[Link](https://arxiv.org/abs/1905.07129)

I did not read it all, just to get the general idea of the method.

## Intro

Pretrained language models rarely consider incorporating kgs, which provide strutured knowledge facts for better language understanding.
They argue that informative enities in kgs can ehnance language representation with external knowledge.

Incorporating kgs into language models propose challenges:
1. strutured knowledge encoding
   - regarding to the given text, how to effectively extract and encode its related informative facts in KGs for language representation models is an important problem 
2. heterogenous information fusion
   - pretraining procedure for language repre. is quite different from the knowledge repre. procedure, leading to two individual vector spaces.

They propose ERNIE which pretrains language model on both text corpora and kgs.
1. they first recognize named eneit mentions in text and then align these mentions to their corresponding eneities in kgs
   - they first encode kg with transe to get the embeddings
   - then they use it as input to ernie
   - based on alignments between text and kgs, ernie integrates entity repre. in knowledge module into the underlying layers of semantic module
2. they adopt masked language model and next sentence prediction as pretraining objective
   - new objective by randomly masking named entities and ask the model to select enenties from kgs to complete alignments.
   - the model needs to aggregate both context and knoledge facts for predicting both tokens and entities

## Method  

Two stacked modules:
1. text encoder
   - capture basic text info from tokens 
2. knowledge encoder
   - integrate extra token oriented knowledge info into textual information from underlying layer
   - so we get unified space for entities and tokens

Given a token sequence and its correspoinding entity sequence, the textual encoder sums the token embedding, segment embedding, positional embedding for each token to compute its input embedding, and then computes lexical and syntactic features.
This is done with BERT.
Then it goes to knowledge encoder to inject knowledge info to language repre.
Entities are represented by embeddings from transE.
Then both output of t-encoder and the entities list are fed to knowledge encoder for fusion.

Knowledge encoder consists of stacked aggregators, which encode enetities and tokens as well as fusing their heterogenous features.

In order to inject knowledge into langauge repre. they propose pretraining task.
Wich randomly masks some token entity alignments and then requires the system to predict all corresponding entities based on aligned tokens.
It also adopts Masked Language Model and text sentence prediction as pretraining tasks to enable ernie to capture lexical and syntactic information from tokens in text.