# Explore Entity Embedding Effectiveness in Entity Retrieval (2019)

[Link](https://link.springer.com/chapter/10.1007/978-3-030-32381-3_9)

### Intro

The paper explores entity embedding in ad-hoc entity retrieval.
Entity embedding learns a lots of semantic infomration from knowledge graph.
Ad-hoc entity retrieval aims to answer user querries throught returning entities from kb.

- Textual fields
  - Previous works represent an entity by grouping entity related    triples into different categories. 
  - The multifield entity representation provides an opportunity to convert the entity retrieval task to a document retrieval task.
  - Therefore, methods like tf-idf, bm25 and sequential dependence models had been used.

- Learning to rank models
  - provide effective way to incorporate different match features and achieve state-of-the-art for entity retrieval
  - these systems only leverage test based matches and neglect semantics in the kb
  - field representation shows its limitation with the structural knowledge representations

- Embeddings
  - TransE - represent both entities and relations as low-dimensional repsentation, then they formalize entities and rels with different energy functions

This work investigates the effectiveness of entity embeddings.
It uses TransE.
Then they calculate the soft match feature between query entities and candidate entities.

They also use previous methods - textual info with multiple fiealds and exact match features with different ranking methods for all fields.
The learning to rank models is used to combine all exact match features and entity soft match features.

### Related work

Entity retrival was first introduced in [14] by using keyword queries.
Existing retrieval systems concern more about the representation of entities.
Some works represent entities ad fielded documents.
Other calculate query and document relevance with a bag of words.
But they disregrard term dependence.
Markov Random field is a theoretical way to model dependence among query terms - variantion is the Sequential Dependence model - which uses unigram.
Entity models extend document models.
They weight all ranking scores from all cathegories - similarity between query and entities - bm25f and mixture of language models.
Thre is also Fielded Sequential Dependence Model.
Probabilistic Retrieval Model for Semistructured Data weights query terms according to document collection statistics.
Learning to rank models such combine features from different models and different fields, which is the best thing.

### Methodology

Three models - text match, entity mention, and embedding model.
Given a query and entity representations, they aim to generate ranking score for entity in the model.

### Text based

Usage of term and term dependence based match features on Markov Random Field model.

- Sequential Dependence Model
  - best described in the paper
- Field Sequential Dependence Model
  - extends SDM with mixture of language model for each field of enetity representation
  - mlm computes each field probability and combines all fields with a linear function
  - it is better than the SDM

### Entity mention based

- Entity Linking incorporated Retrieval model
  - best in the paper itself

### Entity embedding based

Previous models only calculate Q and E correlation with exact matches without considering knowledge based semantic information.
We map the query and entity into the same vector space.
They use TransE.

### Experimental Methodology

There are four types of queries:
1. entity,
2. type
3. attributed
4. relation

They evaluate models from different aspects:
1. SemSeach ES - queries named entity, queries are oriented to specific entities which need to be disambiquated (harry potter vs harry potter movie)
2. ListSearch - combines multiple queries that matches criteria
3. inex-ld - keyword queries with mix of all 4 groups of queries
4. qald-2 - nlp questions with 4 types of questions

Baselines use the previous learning to rank model.
Then they also include entity mention match feature to the baselines.
And also include TransE to the baselines.
So they have one set of features as baseline, then they add entity mention, also they add enetity embeddings.

### Implementation

They use fielded sequential dependence mode as the basic retrieval model to generate candidate entity set with top 100 entities.
Learning to rank are implemented in different toolkits.
TransE model is implmeented in c++.

### Evaluation

Embeddings are great.
The only thing is they first used FSDM to obtain the top 100 result and then used reranking.
What I missed here is whether they could do only single embeddings and not a combination.
The TransE does the best job in inmproving the retrieval.
The most weight in the ranking was given to the transE and FSDM and the baselines too.
The heighest weight is the transE and is more important than the ELR.


The most important paper is which is their previous work [An empirical study of learning to rank for entity search](https://www.semanticscholar.org/paper/An-Empirical-Study-of-Learning-to-Rank-for-Entity-Chen-Xiong/11e1e395431c73a3a961b0c5f30b0227f98873b0)