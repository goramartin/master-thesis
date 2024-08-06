# Search frameworks and ontology ranking

The main idea is to look into approaches that deal with searching ontologies, since there is a necessary step to find classes/properties in them.

Most of the systems here are full-fledged framworks that crawl web for rdf files and ontologies and provide indexing and ranking.
Mostly they create documents from the classes/properties and then use exact match, partial matching to locate the things with tf/idf, elastic search.
They ingest additional relevance for the searching:
- pagerank variants
- centrality measures
- density of the concepts in the ontology (subclasses, superclasses)
- general statistics on the usage of the classes, properties (domain, range), number of instances
- hierarchu similarity of concepts (shortest path between two concepts)
- expansion with how well the ontology covers the topics
- semantic similarity between query and documents
- complexity metrics

Most of the solutions rely that the query match exactly the terms for similarity.
I dont like these solutions that much since they aim at providing ontologies and not the concepts themselves.
But they do provide a sense of what can be important in the ontologies.


- Interesting ideas:
  - can the user select options for relevance?
  - ask for the context before query expansion
  - look at the papers lov, ranking by focus and populariy

<br>

- For diploma
  - popularity:
    - pagerank - swoogle
    - occurences in other documents - falcons
    - centrality - aktiverank
    - importances - ontoQA
    - boosting hihgly reused IRIs - LOV
    - reverse-page rank - DWRank (hubs and authority based on link analysis - more interconnection the better)
    - contxt driven - ontology concept search (pre language models)
    - focus (cue validity based on number of domains of property) - ranking schemas by focus


### Finished

1. [Swoogle: A Search and Metadata Engine for the Semantic Web](https://dl.acm.org/doi/10.1145/1031171.1031289) (2004)
   - it is a crawler of the net
   - they use pagerank to rank the documents - rational pagerank that distinguishes between different edges - **it is popularity**
   - for searching they use traditional ir using n-grams and bag of words for uris - it uses a system with tf-idf techniques
   - for annotations they use text and labels, commets
2. [WATSON: a gateway for the semantic web](https://www.researchgate.net/publication/48989644_WATSON_a_gateway_for_the_semantic_web) (2007)
   - a list of ideas for implementing better search engine than swoogle
   - the idea is to use semantic similarity and topic queries
   - mostly ideas that are not implemented 
3. [Searching linked objects with falcons: approach, implementation and evaluation](https://www.researchgate.net/publication/220123904_Searching_Linked_Objects_with_Falcons_Approach_Implementation_and_Evaluation) (2009)
   - a keyword based search system for linked objects
   - they construct virtual documents for objects (lucene)
   - they do first query similarity based on documents
     -  boosting labels and names since it can get lost in a larger documents
   - then they do also popularity sorting
    - based on the number of occurences of the objects in other documents, essentially it is linking by owl:sameAs
   - they indexed in lucene score(d, q) = query_sim * populariy, simple multiplier 
   - they devices also the weights on the fields
   - they generate human readable snippets for displaying results
   - also allow filtering based on subclasses which people confused
- wighting in 10, 10, 1, 1 - 10 for names and labels
1. [Ranking Ontologies with AKTiveRank](https://link.springer.com/chapter/10.1007/11926078_1) (2006)
  - system for ranking ontologies based on a number of measures that assess the ontology in terms of how well it represents the concepts of interest
  - class match measure 
    - ranking based on matching text in the ontology, the more the better, also exact match is better
  - density 
    - the classes that have more subclasses, properties and siblings, the more the better
    - they did not use instance information since it does not describe schema well
  - semantic similarity between all concepts in ontology
    - based on the shortest paths between concepts
  - betweeness (centrality) of the ontology
2. [Ontology Evaluation and Ranking using OntoQA](https://ieeexplore.ieee.org/document/4338348) (2007)
   - a search engine that is using swoogle to get the ontologies
   - keyword search on the documents
     - keywords are extended with additional keywords using wordnet
   - there are a bunch of metrics that the user can choose from while searching
     - class, instance, properties and global metrics
     - such as population, instances per class, ratios of usages
   - the final score is aggregation of the scores for each found term in the ontology
   - important metrics:
     - class metrics
       - class connectivity
         - number of relationship instances of the class with instances of other classes
       - class importance
         - is defined as the number of instances that belong to the inheritance subtree rooted, i dont like it since the root have the most importance
       - relationship utilizition
         - the relationship utilization on instances ratio with respect to the defined properties
     - property metrics
       - property importance
         - usage on instances 
   - also the score is multiplied by a popularity on a term
   - also discusses why it chose the tf idf
3. [Linked Open Vocabularies (LOV): A gateway to reusable semantic vocabularies on the Web](https://www.semantic-web-journal.net/system/files/swj1178.pdf) (2017)
   - provides a vocabylary management
   - searching concepts based on domain
   - it uses tf idf on terms in a vocabulary with boosting while searching
   - additionally, they use popularity measure for URIs, it gives higher score for terms that appear in many datasets 
4. [ARRO: Novel Approach for Ranking Ontologies on the Semantic Web](https://www.semanticscholar.org/paper/2006-1-St-International-Symposium-on-Pervasive-and-Yu-Cao/dcb6af4aa7779db40a8bbc971cfdd86c1c6b7870) (2006)
   - ranking based on logic view - a relationships to other classes and ontologies
     - a class contains three set
       - properties aquired through domain and range description
       - equivalent classes in the other ontologies
       - other relationships with other classes with the more imporatnce to the hierarchy relations, such as subclass of or intersection of
   - it uses swoogle to retrieve the ontologies 
5. [Ontology-rank - Ontology selection ranking model for knowledge reuse](https://www.sciencedirect.com/science/article/pii/S0957417410011310) (2011)
   - the paper i hate the most
   - semantic similarity between query and concepts in the ontology
   - they are trying to describe semantic similarity on relations to the query - i imagine it as (bob is friend of sara), they sort of of find the endpoints and relation, and the try to give a number to the relation ship
   - problem is that in my case i dont know the names
   - also semantic similarity is cured by the language models nowadays
6.  [OS-Rank - Ranking Ontology Based on Structure Analysis](https://ieeexplore.ieee.org/document/5362262) (2009)
    - the importance of classes in the ontology should not be described by matching the keywords but also structure and semantic rels in the ontology between the class and other classes
    - the metrics are
      -  number of text matches in the ontology
      -  number of subclasses, superclasses, properties...
      -  ranking domain concept
    - i think the most interesting thing was that they proposed wordnet extension
      - they propmpted the wordnet to find similar concepts, and ask the user for better specification of the concept
7.  [Content-based Ontology Ranking](https://eprints.soton.ac.uk/262605/) (2006)
    - They analyzed emails of protege (knowledge graph) and found out that people search using the domain instead of the class names directly
    - Measures how well the ontology terminology covers a given domain
    - they sort of do a query expansion using word net and query google, they pick the top x sites and compute tf idf of the terms in those documents and pick the top 50 used terms as a corpus
    - again as in [9], they asked the user for a specific meaning from the wordnet  
8.  [Content-OR:  An Integrated Ontology Ranking Method for Enhancing Knowledge Reuse](https://www.researchgate.net/publication/289725459_An_Integrated_Ontology_Ranking_Method_for_Enhancing_Knowledge_Reuse) (2014)
    - it is double ranking combination of the [10] and [8]  
9.  [Context-driven Concept Search across Web Ontologies using Keyword Queries](https://dl.acm.org/doi/10.1145/2815833.2816958) (2015)
    - they present a novel concept search approach that exploits structures present in ontologies and constructs contexts to effectively filter the noise in concept search results
    - they argue that the context is not present when searching with text queries
    - they define context as a similar approach from galago
    - assumption is that the input keywords are related
    - i was not very satified with the paper, since it is missing a lot of details
10. [DWRank - Learning Concept Ranking for Ontology Search](https://www.semantic-web-journal.net/system/files/swj883.pdf) (2016)
    - uses simialr metric to page rank
    - it is trying to say what concepts are central to the ontology and combine it how well the overall connection is between other ontologies
      - the more connections the better
    - the initial combinatio

### To read

### To read but with less interest

### For reference

- OntoSelect, OntoKhoj (2008)
  - popularity based the more references to other o. the better.

- [Popularity driven Ontology ranking using Qualitative features](https://orbilu.uni.lu/bitstream/10993/40972/1/2019-07-02_iswc19-ranking-final.pdf) (2019)
  - CARRank, Termpicker, CBRBench, Word2Vec-> popularity based on citations per year and linear trend in citations history, not important to me, but it has a good introduction citating interesting papers and benchmarks
  - it also compares the usage of metrics that were used for ranking
    - the best were wordnet, lucene, understandability
  - it also says things about popularity in the queries
  - cannot use this

- [Ranking Schemas by Focus](https://www.researchgate.net/publication/353514217_Ranking_Schemas_by_Focus_A_Cognitively-Inspired_Approach) (2021)
  - ranking of schemas
  - focus - the state or quality of being relevant in storing and retrieving information
  - defines class importance based on cathegorization of properties on a node (domains). This could be usefull, the problem is how to combine it with the number of properties is wikidata. Also they say it works well with noisy schemas and compare it with TF-IDF, BM25, CMM and DEM.
  - they are trying to define cue validity - informativeness, how much the type is informative in the ontology 
  - the entity types focus, namely, what allows to identify the entity types that are maximally informative categories, which have a higher categorization relevance, or, more precisely, which maximize the number of properties and minimize the number of properties shared with other categories. These entity types being, to some extent, related to what expert users consider as “core entity types” or central entity types for a given domain
  - dont know if this is the best thing, since we dont have a lot of properties on types

- [LOD search engine: A semantic search over linked data](https://link.springer.com/article/10.1007/s10844-021-00687-0) (2021)
  - ranking based on the number of triples in a domain and the number of subjects/objects of triples

- ELECTRE
  -  [A comparative application of multi criteria decision making in ontology ranking](https://link.springer.com/chapter/10.1007/978-3-030-20485-3_5) (2019)
     -  i used this to obtain the good searchers
  - [Comprative ranking of ontologies with ELECTRE](https://www.researchgate.net/publication/365607097_Comparative_Ranking_of_Ontologies_with_ELECTRE_Family_of_Multi-criteria_Decision-Making_Algorithms) (2022)
    - 2022 using complexity metrics for evaluation of ontologies based on CRank (Complexity ranking methods)
  
  - [CRank](https://link.springer.com/chapter/10.1007/978-3-030-00856-7_7) (2018)
    - complexity metrics