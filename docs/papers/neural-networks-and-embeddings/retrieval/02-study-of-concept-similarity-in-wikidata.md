# A study of concept similarity in Wikidata

[Link](https://content.iospress.com/articles/semantic-web/sw233520)

! A big paper !

## Intro

The aim is to estimate concept similarity between nodes in Wikidata.
They say concept similarity should be revisited.
They explore similarity methods in three groups and leverage background information for knowledge injection via retrofitting.
They measure impact of retrofitting with different weighted subsets from Wikidata.

Wikidata is the largest free KB. 
But since it is community driven, it contains errors with challenges - deduplication, blurred distiction between classes and instances and incosistencies in terms of modeling of its knowledge. 
Previously, people focused only on direct tasks:
1. transE and complEx - which organise nodes in geometric space based on structural links to other nodes
2. node2vec - random walk methods - leverage generalizability of language modeling by applpying it to graph nodes instead of words 
3. bert-like - combination of structure and semantics, but it somehow lacks generalizability and robustness

Similarity between concepts in KBs in understudied, but in linguistics it is very popular.

1. wordnet similarity
2. ontology based vector representation models leverage structure in resources like wordnet - random walks
3. pretrained word embeddings
4. models with knowledge injection - again based on things like WordNeet
5. WordType task - translation of word similarity to concept similarity - mapping words to nodes in KB, but its usage is difficult because most methods have been build to work with things like WordNet, since they are curated and clear ontology. They do not have things to benefit instances in Wikidata or similarity of multi word and abstract expressions.

They assume concepts are classes in Wikidata that have instances or subclass relationships.
They design a framework that includes representative similarity metrics based on ontological structure, language modeling, knowledge graph embeddings, and their combinations. We experiment with a novel aggregation method called TopSim, that aggregates over different regions in the KG.
Besides these metrics, we investigate the impact of knowledge injection, where the idea behind is to adapt the precomputed embeddings to a downstream task by leveraging structured knowledge.

## Related work on similarity

(skipping word similarity)

- Concept similarity metrics - corpus based and knowledge based metrics
  - corpus based - text analysis and rely on distributional hypotesis that concept meanings can be inferred based on their cooccurrence in language
    - paradigmatic
      - symbols are regardes as paradigms that are memebers of specific groups
    - syntagmatics
      - are formed between surface symbols to form a syntagm and define meaning of a sentence
    - state of the art are based on the large sclae language models
      - word2vec, glove, bert and roberta
  -  Knowledge based metrics - rely on analysis of ontological structures how concepts relate to each other
     -  graph structure
        -  degree of interconnection captures as - shortest paths, ontology depth, concept specificity and concept density
     - feature based - a concept is a set of features
     - information theory methods - information content of concepts or their common ancestors, where IC is proprortional to all instances of a concept
     - hybrid - combine multiple methods
     - graph embeddings

In the framework they use both main approaches.

- Concept similarity in Linked Data sources
  - matching of ontological schema across multiple knowledge sources
  - load based measure - combination of ontological, classification and property dimenstions of knowledge
  - word nount, word graph, word type - adapting word similarity metrics to concepts,  they combine semantic network structure between concepts with the information content of he concepts, with the follow up wordk - IC of the least common sonsmer of two concepts
  
They address this task with a computational framework that includes metrics based on information content and graph structures, but also metrics based on language models that focus on the literal content present in Wikidata

- Entity similarity in Linked Data sources
  - predicate frequency - inverse triple frequency
  - paritioned information concent semantic similarity - gives more importance to significant relations
  - global vertex similarity
  - most specific similarity query - can estimate similarity of two entities in a single rdf graph
  - linked data semantic distance - direct and indirect relationshipts between two reasources

## Framework

They use graph embedding and text embedding models, as well as ontology based metrics, as initial similarity estimators.
They concatenate the embeddings in order to combine their scores.
They use retrofitting as a knowledge injection mechanism to further tune the individual or combined embedding models through distant supervision over millions of weighted pairs extracted automatically.
The similarity scores generated by the retrofitted embeddgin models can be combined with the score by the ontology based models.

Similarity models are distinguishied into three groups - language models, kg embeddings and ontology-based topoligical metrics.
They employ representative methods from each cathegory and aggregate methods to combine the methods.
They follow a termonology from work [48] and adapt methods and ideas from prior work on word similarity and concept similarity WordNet and DBpedia.

## KG metrics

Previously used mostly for link prediction and node classification which rely on similarity between nodes or graph structures.
Are analogou to the ontology-based vector models in [48].
Metrics group (but only 4 metrics used):
1. translation
2. tensor factorisation
3. random walks models

- Translation models - TransE, ComplEx - simple and intuitive
  - TransE
    - represent graph nodes and relations in the same space
    - triple (h, r, t) - relation r acts as transaltion vector that connects h and t.
    - stems from distributed word representations that capture linguistic regularities in the form of proportional analogies - (keyboard, button) to (office, chair) since they are connect with part-of relation.
    - the embeddings are optimized to h+t and t in space.
  - ComplEx
    - tensor factorisation model
    - complex value embeddings that allow better modeling of asymmetric relations
    - the node and relation embedding lie in complex numbers
    - loss is designed to assign different scores to asymmetric relations depending on the order of the nodes involved in the relation
  - for more look at - Knowledge graph embedding: A survey of approaches and applications
  - they train the methods on all node-node relationships in Wikidata

- random walks models
  - DeepWalk
    - a skip-gram to train over randomly generated sequences of nodes in a KB and generates vectors of nodes involved in that sequence
    - it is analogous to skipgram model in NLP like word2vec
    - it assumes it can be learned though a a stream of relatively short walks which campture neighbourhood similarity and community membership
  - S-DeepWalk
    - tuned to capture structural similarity between nodes
    - two professors may have a high structural similarity if they play analogous roles in their social networks
    - but the graph must be constructed in a different way

## Language models

They use bert models.
Bert is a pretraied network that has been optimized for the tasks of language modeling and next sentence prediction.
Specifically they use Sentence-BErt for sentence embeddings. 
To use these models they had to transcribe the nodes into a natural language.
They use two input variants.
1. human generated abstract
   - Abstract model is based on the abstracts found in the dbpedia.
   - They map these abstracts to wikidata via sitelinks dataset which is avilable on github.
   - For nodes that could not be mapped use concatenation of label and description.
   - From the abstracts they use only first sentences.
2. machine generated lexicalizations based on wikidata.
   - they generate description based on five optional kinds of information
     1. node labels
     2. node descriptions
     3. is-a values
     4. has properties
     5. property values
   - each element is optional and requires specification in terms of which properties should be used for which element
   - the selected things are combined with a template
   - “House cat, domesticated feline, is an organism known by a name, has a heart rate and life expectancy, and is studied by felinology”
   - [lexicalize](https://kgtk.readthedocs.io/en/latest/transform/lexicalize/)

## Ontology based topological metrics

These metrics use feaatures derived from structure of the underlying ontology.
They use two OT metrics.
1.  Information theoretic distance that combines path-based features with information content
    - uses information content of the least common subsumer  given  jc(c1, c2) = 2 ∗ log p(mss(c1, c2)) − (log p(c1) + log p(c2))
    - mss is the most specific subsumer
    - p(c) is normalized probability that a particular concept c is of type c
    - they normalize it to [0...1] by dividing it by the largest distance through the root node in the ontology
2. Class similarity
   - inspired by methods that use IDF for string matching for table linking
   - how?
     - compute set of is-a parents for both concepts based on their instance of and subclass of relations
     - we compute the common parents for both concepts
     - they compute the total class sim score as a sum of the idf scores of the common classes
     - the idf of a class is a ratio between the number of the class instances and the total number of Qnodes in KG  


## Combinations

They just combine the models together.

Similarity functions vary significantly in the kind of similarity they capture.
They are also better at ranking high similarity region than long tail similarities.
They developed top-sim which aggregates different base similarity measures into a combined measure for more robust ranking.
It agregates the measures, and averages over a whole region of high similarity KG nodes for added robustness.
The formula is in the paper

## Knowledge injection

None of the models are directly intended for the task of concept similarity over Wikidata.
Their application to estimate similarity is relatively speaking in a zero shot manner.
They use retrofitting technique for knowledge injection to tune the models to the task of concept similarity.
They experiment with subsets of Wikidata.

They use technique by Faruqui.
It iteratively updates node embeddings in order to bring them closer in accordance to their connections in external dataset.
It is a weighted model.
They take the embedding, take the neighbours of the node, and compute some wieghted average on it and there is a parameter that denotes how much the new vector will resemble those of the neighbours.
They construct some datasets containing only the is a hierarchy and siblings.
Then they use wieghting methods:
1. constant only of 1
2. class similarity between two nodes
3. cosine similarity
But in general they use cosine similarity.


## Conclusion

- Language models:
  - They shown that the best similarity was gained with the simple language model where they use the dbpedia abstracts, better than automatically created lexicalizations.
  - Language model were performing the worst with the labels only.
  - It is important what information should be considered.
- Graph models  
  - The deepWalk performs the best.
  - But all are outperformed by language models
  - Telling us that it adds distraction
  - taken into accound only the relations while disregarding the literals
- Ontology based
  - perform the worst but in one dataset it s better than graph embeddings
- Composite models
  - it is better to combine a small number of reliable models rather than a lot of models
  - it is still worse than the language abstract models despide the fact that they include abstract embeddings inside
- Retrofitting
  - it is good
  - but not a great deal in the methods that include hierarchy already
  - parent-child data was good, siblings did a close to nothing