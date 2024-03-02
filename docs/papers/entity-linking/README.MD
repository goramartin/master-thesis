# Entity linking to Wikidata

It is the task of linking entity mentions to Wikidata entities.
This could be used in the query analyzation process.
E.g. finding entity mentions (classes and properties in the query and then do something like similarity).
The aim is to find something that could be used directly.
This could provide to be usefull with combination of the apporach in Graph empowered entity retrieval.
In which the query is analysed for entities present, then a similarity is done to the candidate set and the entities retrieved from the query.
They used dataset from wikipedia and also the tagger - was tagMe (newer version REL), i tried to use it but received errors or the tagging was not that good.

Or it could be used directly as a search options.

I have read mainly 4 papers on the Entity linking and browsed multiple other ones.
In general, the papers complain, most of the Entity linking focus on Wikipedia (with sometimes linking to wikidata).
The reappearing thing accross the papers is that there is insufficient dataset to do something more clever.
Or the papers focus only on the later second task of entity linking - entity disambiguation - while the mentions are already provided.
But there is a problem with the mention detection, since I could not find a reasonable tool.

Other things, papers I read do not enclose the code, or datasets are only present, code is unmaintained with many issues stating that the code cannot be run or worse everything is missing.
Another big problem is that the things mainly focus on assigning nouns to classes - person, organisation, miscelanous - which is not what i need.
Also, the training dataset (if they exists), focus on finding a limited set of entities from wikidata - persons, org, etc..., while I do need to find general concepts in the sentence.

In this phase, the only workable solutions seemed to be the Falcon 2.
Also a highly available models for end-to-end are: spacy, blink (zero shot wikipedia), failr (wikipedia), lexifuzz (dictionary based), genre (wikipedia, not end to end).

I noticed that there is something different amidst entity linking tools - **zero-shot entity linking**.
Entity Linking (EL) maps an entity mention in a natural language sentence to an entity in a knowledge base (KB). The Zero-shot Entity Linking (ZEL) extends the scope of EL to unseen entities at the test time without requiring new labeled data. 
Which could be usefull to find entities not present in the data.

I found there is a library [zshot](https://github.com/IBM/zshot) from ibm that does exactly this provided the entities have descriptions.
The problem is it does not uses the aliases.
The library seems new (6 moths recent commit).

There is also the [r1] refined, which links to wikidata and allows to use unseen entities (which could be nice), and is fairly new.

- The research ends I guess:
  - try falcon 2, zhot lib (check the properties) and refined libs from amazon
  - the next idea would be to use large language model to find general concepts in the sentence and then create embeddings or use RAG, it would be nice to talk to Necasky and maybe reuse the model for Dominik

### Finished

1. [OpenTapioca: Lightweight Entity Linking for Wikidata](https://ceur-ws.org/Vol-2773/paper-02.pdf) (april 2019)
   - nice approach but old, and they had to create dataset linking wikipedia dataset to the wikidata
   - a working solution but not very good
   - the first solution to appear
   - based on probability models and needs training
   - only includes things that are subclass of humans, organizations and geographical object
   - which makes it difficult to find training data even though they created the datasets
   - there is also a pipeline for spacy
2. [Falcon 2.0: An Entity and Relation Linking Tool over Wikidata](https://arxiv.org/abs/1912.11270) (december 2019)
   - falcon replaces the opentapioca
   - it has better performance
   - rule based approach with dictionaries and works with aliases
   - it also enables to work with aliases and recognize properties
   - second solution to appear - also complains that the neural approaches do not have enough data [r2, 4]
   - the problem is that it works well in sentences, but can be used to recognize keywords
   - the solution is good since it does not need available training data
   - the code seems good enought but issues on github started to appear that there is some error while running the project
3. [Improving Candidate Retrieval with Entity Profile Generation for Wikidata Entity Linking](https://arxiv.org/abs/2202.13404) (2022)
   - the work aims only on the second phase of the entity linking
   - creates profiles of entities based on context and given mention - needs training and dataset, they used wikipedia dataset with linkage to wikidata
   - it assumes the entity mentions are predefines and needs datasets
   - the problem the code is missing and the dataset is not present
4. [Encoding Knowledge Graph Entity Aliases in Attentive Neural Network for Wikidata Entity Linking](https://arxiv.org/abs/1912.06214)  (2020)
   - they use two nn, one for encoding sentence and finding mentions and one for disambiguation
   - all in all they use method of dicionary from falcon (2) as mapping phase
   - they use dataset from wikipedia annotated with wikidata
   - the code is missing and also missing running direction
5. [CHOLAN: A Modular Approach for Neural Entity Linking on Wikipedia and Wikidata](https://arxiv.org/abs/2101.09969) (2021)
  - this is continuation of [4] instead of attentive neural networks they use transformers
  - code is there but no documentations
  - all in all it is trained on t-rex and using candidates using falcon things, arjun [4] had a better performance, again problem is that the entities are just a small percentage of the wikidata 85k entities while the ontology contains 4 milions as of 1.3.2024 

### To read

### For reference

1. [ReFinED: An Efficient Zero-shot-capable Approach to End-to-End Entity Linking](https://arxiv.org/abs/2207.04108)
   - can be used with wikidata and the code seems maintained
   - i looked into the codebase and it seems the model can be trained on the newer wikidata dumps and also extend the with new entities to mention
   - this seems like a good option
   - not sure however if it can handle property detection
2. [A Neural Approach to Entity Linking on Wikidata](https://link.springer.com/chapter/10.1007/978-3-030-15719-7_10) (april 2019)
   - this paper is a predecesor of Falcon 2
   - in falcon 2 they argue that neural methods do not have enough data for training
   - in this paper specifically focus only on disambiguation and not recognition, thus it is hard to use
3. [Tweeki: Linking Named Entities on Twitter to a Knowledge Graph](https://aclanthology.org/2020.wnut-1.29/) (2020)
   - unsupervised
   - tagger from allen nlp library
   - To adapt Intrawiki links to the WikiData KB, we use the existing links between Wikipedia and WikiData entities to gather all the entity aliases and number of time each alias is used in Wikipedia for the entity
   - code is missing only the data are present
4. [Scalable Zero-shot Entity Linking with Dense Entity Retrieval](https://aclanthology.org/2020.emnlp-main.519/)
   - for wikipedia only BLINK facebook
5. [NECKAr: A Named Entity Classifier for Wikidata](https://link.springer.com/chapter/10.1007/978-3-319-73706-5_10)
   -  In this paper they present the tool NECKAr, which assigns Wikidata entities to the three main classes of named entities.
6. [Autoregressive Entity Retrieval](https://openreview.net/forum?id=5k8F6UU39V)
   - genre from facebook
   - only for disambiguation phase 