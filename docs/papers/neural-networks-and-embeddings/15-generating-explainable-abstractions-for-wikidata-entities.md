# Generating Explainable Abstractions for Wikidata Entities

[Link](https://wikidataworkshop.github.io/2022/papers/Wikidata_Workshop_2022_paper_8269.pdf)

## Intro

Wikidata is good.
Usage in downstream applications is beneficial but retrieval and similarity based methods make a limited use of wikidata semantics and lose the link between rich structure of wikidata and decision making algorithm.

In this paper, they investigate how to define abstractive representations of entities.
They propose a method that produce profiles for wikidata entities based on salient labels associated with theri types.

**They create a profile graph from the entities, and compute profile embeddings.**

... back to why the previous methods are bad.
Reasoning systems use metrics that rely on pagerank or learn graph embeddings, encode structure of the graph, but lose much of the information - such as TransE or ComplEx.
It is insufficient, since rich reasoning knowledge is in Wikidata.
Yet, wikidata has no mechanisms to prioritize certain pieces of information in context.

Prior works on summarization aims to provide a substet of knowledge about kg entity.
- Exctractive summarization select the subset based on distinctiveness, frequency, and informativeness, but these have not been applied to summarize entities at scale.
- Absractive summarizations have been built to produce human readable description rather then preserving graph structure.
- Graph profiling is able to provide machine readable summaries for entitiess, but has not been applied at scale.

In his paper they investigate how to define formal repre. of wikidata entities.
They frame the task as profiling from [32] - an abstractive summarization task that aims to create representations that capture the distinguishable properties of an entity.

## 7 requirements

1. salience
   - each entity has various extend of information
   - they want to device strategies to measure salience (dulezitost) for an entity given its context
2. hyper-relational knowledge model
   - wikidat and yago are in a hyper-relational format
     - each edge is associated with additional information, represented as a qualifier
   - profiling should use this information
3. addressing sparsity
   - kg like wikidata are sparse (only 1% of people contain attribute of native language)
   - profiling should work with sparsity
4. explainability
   - understandable by humans
   - not free text but structured
5. scalability
   - wikidata is large
6. utility
   - it should be easily usable
7. customizability
   - to suit different needs profiles can be parametrized and be usable possible on different kg
   - meaning code should be transparent

## Profiling  

A profile consists of a salient property-value pairs for an entity type.
A set of profile statements **(labels)** in wikidata are of the form <t, r, v>, where t is an entity type in wikidata, and p is property, v can be numeric, range, entity, or label with interval or numeric value.
Entity profile is a union of the profile labels **for all its semantic types**. 

- 6 steps:
  - preprocessing
    - they use a subset of entities from which a small number of very populous classes of entities have been omitted
      - The subset was taken from the 2021-02-15 Wikidata dump, omitting entities of the classes Scientific Publication (Q591041), Star (Q523), Galaxy (Q318), Review Article (Q7318358), Gene (Q7187), Chemical Compound (Q11173), and Protein (Q8054). The subset is available here: https://drive.google.com/drive/folders/1cwLwzoamRVDKB5oG_Mxj_bdK1FGdzmdd?usp=sharing
    - swich date time values to years
    - unit values are defined by properties - mass in kg vs mass in lbs, are new properties and uncomparable
    - in general they keep the most up-to-date data
  - label generation
    - generating large pool of labels from wikidata
    - 2 substeps:
      1. associate each entity to its semantic types
           - we have instance of and subclass of
           - based on these relations over 2 million nodes in wikidata serves as classes
           - dbpedia has less than 700 classes
           - they generate links only based on direct p31 links
      2. query wikidata to generate type-based profiles, for each value type in labels
         - attribute-valued and relation labels are obtained directly through graph patterns
         -  within attribute valued they discard string values, as it is unclear how these would contribute to the utility of profiles
  - label filtering
    - to support salience requirement they filter out labels with extreme frequencies
    - e.g. labels which are extremely frequent (humans being instances of humans), as these are trivial
    - also they filter out labels wich are extremely rate, since they are not representative
    - they generally define a support parameter, which captures percentage of entities of the label's type that the label is applicable to (which means they define appropriate range)
    - sparsity of wikidata could lead to a large imbalance across entity types, as well populated entity types (human) will have many more labels compared to more sparse types (fictional character in musical work), these factors can cause labels to applu to a smaller percentage of entities, making it more difficult to filter out unrepresentative labels without
    - so they define support threshold for each value type favoring value types which can be more useful over non discretized variants and two hop structures which are less intuitive to humans
  - embedding creation
    - they train random walk embeddings of wikidata nodes in order to assess their distinctiveness
    - they consider three types of walks based on - homophily, numeric attributes, and graph structure
    - the walks generated by each method are passed into a skipgram model in order to create corresponding embeddings
      - homophily is generated directly on wikidata subgraph of entity to entity relations, which is identical to deepwalk
      - attributative - they propose to discretize attributes of each entity into percentile bins
      - structural - they define allowed hops for each entity, they seek structurally similar entities
  - profile curation
    - because node embeddings natively capture entity similarity, they use them to compute distintiveness of each remaining label
  - profile embedding creation
    - they construct a profile based knowledge graph, where wikidata entities and profile-label-ids are nodes, and edges are used to connect entities to their profile-label-ids and profile-label-ids to the profile labels information.
    - not going to write it all

## Evaluation of entity similarity

They computed similarity between certain things based on some wordsim dataset.
They found out that the best similarity is based on class hierarchy for instances.
The second one was ComplEx embeddings and the third one was very close to the ComplEx and it was Profiles, which means that comples and profile capture similar information.
The problem with this method to use it for me is that is it is ment for instances and not types.