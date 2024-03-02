# CHOLAN: A Modular Approach for Neural Entity Linking on Wikipedia and Wikidata

[Link](https://arxiv.org/abs/2101.09969)

## Intro

EL - given a sentence, identify mentions, map these to most likely entities, disambiguate.
The El are cathegorized: 
1. intial atempsts solve separate problems
   - errors propagate
2. joint modeling of md and ed
   - depend on an intermediate candidate generation and rely on precomputed list of entity candidates 
3. combination of all into a joint model

Recent approaches focus on jointly modeling two or three subtasks.
Usage of transformers were used.
But were not that good than [End-to-End model for neural entity linking].
In this paper they focus on understanding bottlenecks of transformer based models.
They argue that candidate generation is less studied.

They hypotesise that transformers need additional task specific contexts, including context at ed may impact performance.
They deviate from modeling the subtasks jointly and treat each subtask independently.

They propose cholan as a modular approac of two transformer based models to solve md and ed.
They use bert to identify mentions, then they do mapping and lastly entity mention, sentence, candidate and wikipedia entity desc are fed as input sequences in the second bert based model to predict entity.
They train steps independently.
While testing, they run the pipeline end-to-end.

Apparently it is made so it can be easily transfered to additional knowledge base.

## Related work

- Skippnig NER.
- Candidate generation
  1. matching mentions to a predefined candidate sets
  2. dictionary lookup
  3. empirical probabilitic entity map
  4. local kg with entity mentions using wikidata with entity labels and aliases
- Skipping end to end

## CHOLAN

### MD

They use bert for notifying entity mentions in text.
They append CLS and SEP to start and end of the sentence respectively.
This is used as input to the model which learns a represenation of the tokens in the sentence.
Then the nn leanrs repre of tokends in the sentence.
They introduce classification layer on top of bert to determine named entity tags for each token following bio format.
Model is used as baseline and finetuned for detecting entity mentions.

### CG

- DCA candidates
  - probabilitic approach to calculate prior probabilities of candidate entities for a given mention.
  - In eac prob. entity map, each entity has 30 potential entity candidates
  - they also include wikipedia description
- falcon 
  - local index of kg items from wikidata
  - they build a predefined candiate set using the top 30 wikidata entity candidate set for each entity mention.
  - they enrich entities by correspondence from wikipedia
  - they also add wikipedia first paragrraph of as entity desc to the hyperlinks

### ED

They propse wikiBert.
Induction of local sentential context and global entity context at the ed in a transformer model.
Derived from vanilla bert and finetuned on the two el datasets.
They view the ed task as sequence classificatoin task.
The input is comb. of two sequences.
The first concatenates the entity mention and sentence in which it was found.
The second concats candidate and its correspoding wikipedia description.
The two sequences are paired together.
They train the model using negative sampling.
The candidate list is generated for each identified mention.
The desired item is labelled as one, the rest are zero.

## Set up

They use t-rex dataset of wikidata.
It has 780k sentences in training and 196k in test, and links to 85k entities.
Which is not much.
For wikipedia I dont care.

## Comparisons

Opentapioca is a baseline.
And arjun.

1. Train the model using T-rex and falcons map without wiki descp if missing.
2. On wikipedia with falcon with sentential context and no desc.
3. They use probabilistic candidate set with wikipedia context and desc.
4. Same as 2 but add description.

## Evaluation

Arjun has better f1 score.
Wikidata is challenging since many labels share the same name.
They did not do pretraining (sota on wikipedia) since it is bound with wikipedia data and methods.

IDC about wikipedia.

## Comments

They use induced contexts thanks to modular architecture.
Using plug and play candidates resultined in significant increase in performance.
In earlier versions the things are monolithic.
It needs training.
It needs wikipedia descriptions, but wikidata description could be used instead.


