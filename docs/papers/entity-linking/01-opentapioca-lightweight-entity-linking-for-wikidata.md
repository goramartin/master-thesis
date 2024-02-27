# OpenTapioca: Lightweight Entity Linking for Wikidata

[Link](https://ceur-ws.org/Vol-2773/paper-02.pdf) (april 2019)

## Intro

It is a simple named entity linking system that can be trained from Wikidata only.
It is also possible to keep it synchronous with wikidata in real time.
Most previous works focus on other KB.
Wikidata is editable and multilingual.
They review the main differences between wikidata nad static knowledge bases.
They ilustrate the differences by building a simple entity linker.
The linker only uses data from wikidata.
It can be trained only from the dump.
They also propose tools to adapt existing entity linking datasets to Wikidata.

## Related work

Entities in kb are associated with a set of possible surface forms.
Given a text, the annotator looks for occurences of their surface forms in text.
Many matches can be false because of homonymy, so the matcher is learnt to predict correctness.
Usually they use features:
1. local compatibility - assessment of adequacy between entity and phrase, relies on dictionary, this approach also counts number of occurences of entity by a phrase
   - in wikipedia it can be done extracting mentions from link labels, redirects, disambiguation pages and abstracts
   - in wikidata labels, and alisases are of good quality, but counting occurences is difficult, also two entites can have the same label
2. topic similarity - topic with the text and topic with candidate entity
   - estimated with similarty measures - tfidf or keyword extraction
   - it consists of structured data and the methods above are difficult to use
   - vectors can be used but dunno how to compare them to topic
   - neural word embeddings were used to represent topical info for text and entities, but it requires a large amount of text 
3. mapping coherence - entities mentioned in the same text are often related so linking decisions are inter-dependent
   - to miximize topical coherence in chosen items
   - there is some metric on wikipedia, but it cannot be used on wikidata since it has different structure
   - once the method is chosen it needs to be intergrated with the inference process
   - most approaches build upon graph of entities candiates, where edge means sematic relatedness, then a approximation to find densest subgraph

## Method 

They propose approach that adapts previous methods to wikidata.
They take a document and find spots in it, the spot defines a phrase and for that phrase we get entity candidates - entities that have label or alias in the phrase.
Given to spots, they build a biinary classifier to predict for each spot in document and entity candidates in the phrase.

- Local compatibility
  - htey estimate popularity of entity and the comonnonss of the phrase separately
  - popularity is log-linear combination of its number of statements, sitelinks and page rank score, page rank is done on entire wikidata using statement values and qualifiers as edges
  - the phrase commonness is estimated by simple word unigram language model that can be trained on any large unannotated dataset
- Semantic similarity
  - features above ignore the context
  - general idea is to define a graph on the candidate entities, linking candidate entities which are semantically related, and then find a combination of candiate entities which have both high local compatibility and whichc are densely related in the graph
- Classifying entities in context
  - first combine local features into a local evidence and then spread this local evidence using markov chain

## Experiments

They had to create a dataset for wikidata.
They took one from dbpedia and converted it - by linking links from dbpedia entities to wikidata, then openrefie to extract entities which were not linked, and human review.
They also made dataset of autohor affiliation strings extracted from research articles and exposed by istex text and data mining service.
They indexed the wikidata json dump with SOlr, they restrict the index to humand, organizations and locations by selecting items whose type was subclass of human, organisation and geographical object.


## Comments

This is somewhat nice approach but old.
Code is on github, but it only includes things that are subclass of humans, organizations and geographical object - which makes it difficult to find trainning data even though they created the dataset.