# Linked Open Vocabularies (LOV): A gateway to reusable semantic vocabularies on the Web

[link](https://www.researchgate.net/publication/312015882_Linked_Open_Vocabularies_LOV_A_gateway_to_reusable_semantic_vocabularies_on_the_Web)

## Intro

The web needs a vocabulary management. A vocabulary defines the meaning of data.
Some are not published or lost -> the data is loosing semantic meaning and interoperability.
The purpose of LOV is to promote and facilitate the reuse of well documented vocabularies in the Linked Data ecosystem.
It provides:
    - Ontology search - searching vocabulary terms based on domain (the vocabularies are cathegorized according to the domain they address)
    - Ontology assessment - a ranking or each term retrieved by a keyword search
    - Ontology mapping - 7 types of relationships between ontologies - metadata, import, specs, gens, extensions and equivaleence used for aligments


## Extraction and building

- At the vocabulary level it explicitely extracts
    - it extracts the metadata mentioned in the vocabulary (things from dublin core) 
    - inlinks to other vocabularies 
    - outlinks to other vocabularies
- Then it extracts relationshipts mentioned above and includes then with the Vocabulary of the Friend (VOAF)
- Then it goes to term level analysis
  - it extracts
    - term type (class, property, datatype, instances) in the namespace of vocabulary
    - natural language annotations (rdf literals), later used for scoring
    - pupularity - info taken from LODStats project (not so mucj more info on this)

## Ranking and search 

(The formulas are explained in nice detail on page 8 and 9)

  - ranking method adapting "term frequence invese document frequency" - "tf-idf" to the graph structure of vocabularies. It takes into account relevance and importance of a resource to the query when giving a weight to a vocabulary for a given query term. Also, reuse augmented frequency variations of term frequency formula to prevent bias towards longer vocabularies.
    - the basic unit is not a word, but a vocabulary term *t* in a vocabulary *V*.
    - popularity measure - function of normalisation of the frequency of a term URI *t* in the set of datasets and normalisation of the number of datasets in which a term URI appears. This measure will give a higher score to terms that are often used in datasets and across a large number of datasets
    - then there is also extension of field-length norm from ElasticSearch, which attaches a higher weight to shorter fields by combining it with a property level boost. Using the boost they can assign a different score depending on which label property a query term matches (e.g. local name, primary labels, secondary labels, tertiary labels...)

- Everything is indexed and full text search is provided + users can add terms to narrow down the returned results.
- The final score for a *t* for a query *Q* is combination of the tf-idf, the impotance of label properties on which query terms matched and the popularity of that term in the LOD dataset.  The popularity metric provides an indication on how widely a term is already used

## Conclusion

To sum it up - they use tf-idf with normalisation and popularity measure.
During this paper they mentioned a popularity a lot of times - why is it important - look at [9] and [26] as mentioned in the paper.

This paper also contains a lot of information on the entire architecture - but for my purpose I wrote down things only for the searching. 

Other search engines - swoogle, watson, falcons offer filtering based on ontology type (class, property) and ranking based on popularity but they dont look for ontology relations.
 