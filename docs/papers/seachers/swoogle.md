# Swoogle: A Search and Metadata Engine for the Semantic Web

The Swoogle is a crawler based indexing and retrieval system. It extracts metadata for each discoreved document and computes relations between documents. 
Documents are indexed and N-Gram or URIrefs as keywords are used to find relevant documents and compute relevance between documents. 

It has a web view of the semantic documents.

- Tasks to fulfill
  - Finding appropriate ontologies
    - finding ontologies that contain specified terms - either contain or are about the term
    - the returned ontologies are ranked based on "Ontology rank" (their own alg.), which takes into account the usage by the communnity.
  - Finding instance data - enable queries that constraint classes and properties used by documents.
  - Characterize the Semantic Web - by collecting metadata

- Collecting document metadata
  - Basic - language,  statistics and ontology annotations
    - language - syntactic or semantic features
      - encodings - rdf types or xml
      - language of the document - owl, daml, rdf, rdfs
      - owl species
    - statistics - summary of node distribution of rdf graph inside the document
      - Ontology ration - the portion of properties and classes in the entire doc.
      - annotations - label, comment, versionInfo
- Relationships among documents
  - term reference by uris
  - imports of another ontology
  - extensions of ontologies
  - versionning - prior, compatibility
- Ranking of crawled documents - relative importance of web documents based on PageRank -> rational random surfing model
  - we are classifying inter document links between two documents
    - imports entire content
    - uses term without import
    - extends
    - asserts
    - the total number of references
  - theses are four cathegories  -> the mains are the imports and extends -> they give weights to them
  - THe random surver can jump directly to document with probability *d*, while link following gives us unequal probability, *-f(x,a)/f(x)*, *x* is the current doc, *a* is the doc that *x* links to, *f(x,a)* is the sum of all link weights from *x* to *a*, *f(x)* is weight of all outlinks from *x*.

- Searching
  - n-grams - segment of the text which spans inter word boundaries - sliding window
    - it should be better than matching whole words