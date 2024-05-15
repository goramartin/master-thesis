# RAG with neo4j

[Link](https://www.linkedin.com/posts/jbarrasa_advanded-rag-with-knowledge-graphs-ugcPost-7139723682007920640-q9cA)
  - [youtube](https://www.youtube.com/playlist?list=PL9Hl4pk2FsvX-5QPvwChB-ni_mFF97rCE)

## Intro

The link links to series of knowledge graphs and embeddings.
It walks through a simple applications to advanced patterns.
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

## Lesson 22. rag with knowledge graphs

Retrieval augmented generation with knowledge graphs.
We want to use LLM in our applications, but the LLM are build on top of general information and probably out of date, they will never have all the facts, since they are built on public data, we want to use enterprise data.
SO we watn to use LLM but use the facts we have in our enterprise.
There are problems with the halucinations, we want to turn down the creativity - do it based on the context i give it to you.

1. we want to ask llm a question
2. then we want to access external storage, going out and get all the relevant information - context
3. i am going to pass the context on with the question

- How the most simple solution works?
  - normaly you use vector based representation and sent to a vector database
  - this will give us a number of approximate results
  - it is critical to get the best information since the data that are passed to the language model is limited + it can take a long time

- How do KG improve RAG? 
  - by making retrieval structure aware 
    - we have neo4j graph, ideally we would like to pass the entire data to the llm
    - we want to do chunking unstructured data into fragments - imagine keeping some base information but always provide certain part of the knowledge (e.g. based on some cathegory)
    - some of the data with vectors might not be picked up se we can use graph and see related things
  - enabling context augmentation
    - use information in the graph, not just vectors
    - sort of template patterns
      - parent
        - navigate to parent and get the context around
      - we have a text and ask the llm to create hypotetical question and annotate the graph with the question, then we can match the question based on the vectoried questions
  - fine grained access control
    - you can get certain visibility based on your access rights 

Now it is time for some code.
They use examples on articles from previous lesson.
The main idea is that they use for some recommendations on articles: i am reading this article, give me articles that i should read based on the one i am reading.
They first query the vector index to get the similar articles.
Then they sort of pass the arcitcles with summary to the llm and ask for the best one.

To move from the vector based search, they use taxonomy similarity and sort of build explanation based on the graph strcture using properties and nodes and type (they are building text representation of the similarity).
E.g. original article mentions this explicitly, the recommended article mentions this explicitly, type of etc...

## Lesson 23. Advanced RAG patterns with Knowledge graphs

We continue right where we left it.
A rag is architecture - using language models and external resources.
Today we will combine the previous two solutions - vector and graph rag.
The idea is that we first do semantic search on vectors and then dereference the nodes and obtain additional information which will be the context to the llm and ask the question with it.

1. example
   -  QA on document with rich internal resources - imagine some pdf - we want to ask question about some definition - and we rag the shit out of it
      - we have sections, parts, definitions
      - chunking the document and create a vector index
      - we will see the document as a tree
   - They will use langchain in this lesson.
   - They will create the index using a langchain.
   - They are showing a creation of index with langchain neo4j.
   - Essentially, they have a graph, and then they query the graphs embeddings based on vector similarity and question.
   - What then they need to do the rag and essentially create response based on the retrieved passage.
   - Okey, now they did this, but they want to enrich the context they will input to the llm with query - the pdf contained definitions but it was somewhat split into multiple parts thanks to chunking - so they want to retrieve the entire definition from the graph store. 
2. example 
   - an art gallery assistant that will generate some personalized email
   - we will give the facts to the llm 

## Lesson 24. Ontology driven RAG patterns

Previously the contextualize query was fairly rigid, the question for today is how to make it a bit more dynamic.
Previously application on lesson 15 they created a streamlit app which did not have a lot of logic code, but had a representation in data (ontology), so there were no specific target queries.