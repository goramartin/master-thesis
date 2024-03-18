# CAR-rank: Identifying Potentially Important Concepts and Relations in an Ontology

[Link](https://www.semanticscholar.org/paper/Identifying-Potentially-Important-Concepts-and-in-Wu-Li/4f713a8b72dafa9bfdb64bb967f1e96de5156775) with connection to DW-rank as it uses reverse page rank as well, but simillar.

## Intro

They propose four features to mark potentially important concepts and relations.
Then they use a simple ranking algorithm to rank concepts and relations altogether.
The importances of concepts and weights of relations reinforce one another in iterative fashion similar to Page rank algorithms.

Before the importance of concepts was measured by browsing activities of users or hierarchies but it is missing correlation between concepts and relations.
This papers adds that, with the intention of promoting exploration and reuse.
They use graph structure of the ontology to introduce importance ranking model, the model tries to imitate the creation process of an ontology from the ontological structural point of view by defining four features.

The algorithm is called CARRank and is simillar to PageRank.
It is iterative and the importance and weights grow iteratively.
The direction of walk for the algorithm is opposed -> which is better for ontology understanding (it is convergent).


## Related work

- cognitive support for ontology understanding
   - There was an importance metric based on the interest among users, which reminds me of popularity in other metrics \[7 - protege module\]. The [20] does the thing based on hierarchy.
   - the difference is that importance of one concepts should take into account all other concepts through relations

- ontology ranking
  - OntoSelect, OnthoKoj based on popularity
  - AktiveRank based on centrality
  - the aim of ther work is the granularity - here they aim at concepts

- Two approaches from the web:
  1. PageRank
     - a good authority page is pointed out by a many good authority pages. And computation is done in random surfer
  2. HITS
     - mutual reinforcing relationship between hub pages and authority pages withing a subgraph
   - These two were combined into a Reverse Page Rank, which is a similar method used in this paper, and also in the DW-rank, except they do not work with hyperlink but ontology relations -> subclass, superclass, property of... which each carries a different weight in the algorithm (ObjectRank [3]).
   - there is also objectrank and poprank but they need prior knowledge and weighting which is not common

## Model

It is based on the stream of conciousness.
The idea is that we are somehow ranking based on retracing creation of the ontology with regard to four features:
1. A concept is more important if there are more relations starting from the concept
2. A concept is more important if ther is a relation startgin from the concept to a more important concept
3. A concept is more important if it has a higher relation weight to any other concept.
4. A relation weight is higher if it starts from a more important concept.

The meaning of importance is that the author wants to suggest something to the user.
A concept is a source that owns a set of relations related to other concepts.
Concepts and relationship exhibit a mutually reinforcing relationships.
In this paper, term importance is used as a metric for measuring the extent that the ontology creator suggests a concept or relation to users.

## CARRank algorithm

We define adjancency matrix representation for the graph (the basic as we know from graph theory).
We define relation weight function w(v_i, v_j), and w_i_j = w(v_i, v_j) be the weight of all relations from v_i to v_j.
Then we make matrix out of it, the same as adjancency matrix.
For each concept we define relevance function r(v_i) and r_i = r(v_i), is importance value of v_i.
Sum of all importances is 1.
The relation importance vector for a concept is (r_1 * w_i_1, ..., r_n * w_i_n) - we multiply it for each concept by the weights of relations to other concepts -> some can be zero if there is no relationship. 

The computation is the reverse PageRank like.
The difference is that it updates the weight of relations during the iteration according to the last two features of the model.
The rest of the algorithm is on pages 41 and 42 since everything is important.

## Experiments

We want the lowest number of iteration for convergations.
For measuring quality they employ a variant first 20 precision metrics.
Ranking methods:
 - they choose page rank
 - the importance based labeling from hierarchy approach
 - aktiverank
To obtain results they asked people to rank the concepts -> get the top 20 from the given ontology.
The CarRank and aktive rank did a good job.

## My comments

It is hard to say it is importance to my use case, since defining importance in the Wikidata could be error prone thanks to a lot of semantic and structural errors.
While keeping in mind, that searching is based on query - one might say - that the number of edges on the concept, does not mean entirely, that it is somewhat worse or better from the search point of view.