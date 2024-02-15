# Content-based Ontology Ranking 

[Link](https://eprints.soton.ac.uk/262605/)
[Presentation](https://protege.stanford.edu/conference/2006/submissions/slides/11.1_alani-slides.pdf)

## Intro

This paper presents a paper that obtains a list of ontologies from a search engine that contain the terms probvided by a knowledge engeneer and ranks them.
The ranking is done based on how many of the concept labels in those ontologies match a set of terms extracted from a corpus of documents related to the domain of knowledge identified by a knowledge engineer's original terms.

Why is it done this way?
    - They analyzed emails of protege (knowledge graph) and found out that people search using the domain instead of the class names directly.
How?
    - they define a content similarity of an ontology to a corpus that is selected for the given search terms
    - the corpus is selected based on the user query
    - they pick up domain related terms and use the for evaluating selected ontologies in terms of how well they cover the domain of interest
    - they extract the terms using tf-idf, and the terms with the heighest score are considered as a potential concept labels
    - they pick 50 top terms
    - the ontology with the most matching terms is the best one

## Obtaining a corpus

They use google search and pick the first 100 pages as a corpus.
But this was bad since the results were too general.
Then they used WordNet to expand user search terms.
And after that they used the google.

## Ontology score

They use class match score - CMS (something similar was done in Aktive-rank).
They also search comments and literal values (LMS) in the ontology to see if they match the selected corpus terms.

> Note for experiment: in one experiment they used pages restricted to wikipedia pages