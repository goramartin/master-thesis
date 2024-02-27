# Falcon 2.0: An Entity and Relation Linking Tool over Wikidata

[Link](https://arxiv.org/abs/1912.11270) (december 2019)

## Intro

The first joint entity and relation linking tool over Wikidata.
It receives a short natural language text in english and output a ranked list of entities and relations annotated with the propert candidates in Wikidata.
Candidates are represented by their IRI in wikidata.
Falcon resorts to enlighs language model for the recognition task, and the an optimalization approach for the linking task.
It outperforms existing baselines.
It is open source and can be reused by the community.

NED consists of two tasks - recognitions (identify entity surface forms) and entity disambiguation (linking  surface forms to semi structured knowledge repositories).

Based on previous approach on Falcon Dbpedia.
Two main concepts: 
1. linguistics based that relies on several english morphology principles sych as tokenization and n-gram tiling
2. local knowledge base which serves as a source of background knowledge (previously kb of dbpedia)
They try to do it on wikidata.

It is able to recognize entities in keywords with no relation.
It outperforms all existing baselines.

They created a new background KG for falcon 2.
They extracted wikidata entities from its public dump and aligned these entities with the aliases  present in wikidata.

## Related work

Online forums and repos for linking over kg exists.
There are deep learning meethods end-to-end that do both ner and ned in a single step.
NCEL leanrs local and global features from wikipedia articles, hyperlinks and entity links to derive joint embeddins of words and entiteis.
These embeddings are used to train GCN, that integrate all features through multilayer perceptron.
Output is passed through sub graph convolutions, which resrots to a fully connected decoder.
BI-LSTM-CRF formulated entity linking as a sequnce leaning tasks in which entity mentiones are a sequence whose length equals to the series of the ouput entities.

- **But these methods high quality traning annotations which are not extensively available for wikidata entity linking.** 
- This links paper A Neural Approach to Entity Linking on Wikidata [6]
- and a paper  Encoding Knowledge Graph Entity Aliases in an Attentive Neural Networks for Wikidata Entity Linking
- There is evidence that machine learning mdels trained over  generic dataset such as wikidis, conll, do not perform well when applied to short texts.
- Entity linking over wikidata is a new domain.
- A paper [6]
  - proposes a neural network based approach for linking entities to wikidata
  - they align existing wikipedia corpus based dataset to wikidata
  - this work assumes only entity disambiguation and assumes that entities are already recognized in the sentences
- A paper [19]
  - attention based neural network for linking wikidata entity labels
- Opentapioca is another attempt to perform end to end entity linking and is closes to Falcon 2
  - Does not provide relations
  - and is used as a baseline

## Falcon 2

### Architecture

It receives short texts and outputs a set of entities and relation extracted from the text, each entity and relation in the output is associated with a unique IRI in wikidata.
Falcon 2 resorts to BK and a catalog of rules for performing entity and relation linking.
The BK combines wikidata labels and their aliases.
Additionaly it comprises alignments between nouns and entities in Wikidata.
Alignments are stored in a text search engine, while knowledge source is maintained in a redf triple store.
The rules of morphology are in a catalog - a forward chaining inference process is performed on top of the catalog during extraction and linking taks.
There exists modules that identify and link entities and relations to Wikidata.

### BK

They extract only labels to create local BK.
They work with synonyms from aliases.

### Catalog rules

It is a rule based approach.
English morpholoical rules are borrowed.
It exludes all verbs that are not entities.

### Recognition

Three modules:
1. POS 
   - gets text, as an input, it tags each word in text with its related noun, verb, adverb
2. tokenization and compounding 
   -  builds token list by removing stop words
3. N-gram tiling
   - combines tokesn with only stop words between them relying on the rules from catalog.

### Linking

Four modules:
1. candidate list generation
   - receives output of recognition phase
   - the module queries text search engine for each token
   - tokens will have associated cnadidate lists of resources
2. march and rank
   - ranks candiadate list received from 1.
   - ranking in form of triples
   - checking if the triple  the module chcekcs if the triple exists in rdf triple store (wikidata) by doing ask query 
3. relevant rule selection
   - using catalog rules, do rank increments 
4. n gram splitting
   - is used if none of the triples tested in matching and ranking 
5. text search engine
   - stores all alignments of the labels
   - a simple quering technique is used as the text search engine over background knowledge (in elastic search)

## Experitments

OpenTapioca bad.
Falcon good.

Problems with falcon is the limitation on gramatically incorrect questions.
Problem is the limited context senteces.
WIkidata has problem with vandalism.
Rules based approached have its limitations when the sentential context is minimal but these approaches are good for nonavailablilty of training data.