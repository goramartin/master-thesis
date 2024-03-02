# RAG with neo4j

[Link](https://www.linkedin.com/posts/jbarrasa_advanded-rag-with-knowledge-graphs-ugcPost-7139723682007920640-q9cA)
  - [youtube](https://www.youtube.com/playlist?list=PL9Hl4pk2FsvX-5QPvwChB-ni_mFF97rCE)

## Intro

The link links to series of knowledge graphs and embeddings.
It walks through a simple applications to advanced patters.
It is made by neo4j and the tools used are focused on neo4j.
I picked a few lessons.

- Lessons to my interest:
  - 16. semantic similarity metrics in taxonomies
  - 21. vector based semantic search and graph based semantic search
  - 22. rag with knowledge graphs
  - 23. Advanced RAG patterns with Knowledge Graphs
  - 24. kg+llms ontology driven rag patterns

## Lesson 16. Semantic similarity metrics in taxonomies

We measure similarity between elements in the taxonomy.
We are assuming the tree structure, but could be done on any graph with errors.
We are looking at some distance metrics.

- We will be talking about three similarity metrics comming from linguistics:
    - path similarity
      - distance between the elements - finding the common ancestor or `(1/(1 + dist(a,b)))` boot eventually
    - leacock-chodorow
      - taking into account depth
      - `-log(dist(a,b) / (2 * depth(t)))` 
    - we-palmer
      - using depth of the least common ancestor
      - and depths of the two concepts
      - `(2*depth(lcs(a,b))) / (depth(a) + depth(b))` 

In the tutorial they will use wordnet corpus for examples.
Wordnet is a collection of synsets - a collection of words that have the same meaning.
They show that the word dog can have multiple meanings.
The wordnet maintains a graph of the words as in hypernyms (less specific) and hyponyms (more specific).

They complain that tools lack these things.
They use ttl of classification of vehicles.
They use that neo4j can import ntl files.

## Lesson 21. Vector-based semantic search and graph-based semantic search

Difference between between graph-based and vector-based semantic search.
One based on vectors and one based on graph structure.

To understand semantic search we need to understand semantic similarity.

- Data representations:
  - symbolic representation 
    - e.g. were  graph, string, etc... fit
    - graph similarity on taxonomies - graph can provide context that explains semantic similarity on concepts (we dont do string similarity and move on meanings)
  - subsymbolic representation
    - as vectors in machine learning

Why graphs? - graphs are easier to explain than vectors, since we can see the graph and follow it.

- Running example
  - unstructured documents
  - we extract entities from it and enrich it with ontology
  - when we have these we can find semantic similarity

They mention that neo4j has vector index.
They can add vectors as properties on nodes and index them.


- Example (the loading was done in the 2. lesson, it is similar to graph-empowered entity retreiva paper):
  - they load articles into neo4j
  - they load context (like wikidata), extract ontology from wikidata using sparql on articles
    - they also do a cleaning to remove shortcuts in the graph
  - apparently it is a separate graphs?
  - then they had the context as a graph and the articles, now they want to extract entities from these articles that are mentioned in the text
    - the extraction is done using the NLP wrapper for neo4j for the main cloud providers
    - in the example they run the google cloud api
  - then we want them connect it to the context
  - after the connection they vectorize the articles and store the vectors in the nodes
  - they start computing similarities
    - it will do not give us reason we it is similar
    - thats why they use graphs