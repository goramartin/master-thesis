# 6. meeting

This meeting I would like to talk about:
1. Brief overview of what I did.
2. State of research project
   - Examples of instances
   - Literals
3. Testing

## Brief overview of what I did

- [x] Finishing up programming part of research project -> tomorrow. 
- [x] Think about testing.
- [ ] Think about diploma text.

## State of research project 

1. Programming part finishing up tomorrow
   - Missing
     - Examples of instances
     - Entity detail 
2. Domains/Ranges of properties inside Dataspecer
   - in core/v1 a property cannot have multiple domains/ranges
   - "ohekováno" with iri 

### Examples of instances

- [Link](https://query.wikidata.org/#SELECT%20%3Finstance%0AWHERE%0A%7B%0A%20%20%7B%20%0A%20%20%20%20wd%3AQ41576%20%5Ewdt%3AP279%2a%2F%5Ewdt%3AP31%20%3Finstance%20.%20%0A%20%20%7D%20%0A%20%20union%0A%20%20%7B%0A%20%20%20%20%3Finstance%20wdt%3AP31%20%3Fancestor%20.%0A%20%20%20%20%3Fancestor%20%5Ewdt%3AP279%2B%20wd%3AQ41576%20.%0A%20%20%7D%0A%20%20filter%28strstarts%28str%28%3Finstance%29%2C%20str%28wd%3A%29%29%29%0A%7D%20limit%205)
- Sometimes takes too long
- Sometimes the instances are not so representing
- Maybe instead of providing a list of example instances which might be "bad"
  - provide help box how to find them
    - link to run the sparql query
    - examples of how to search the main wikidata search
      - haswbstatement:P31=Q8054

### Literals 

- Until now literal, properties mapped to ofn basic data types
- [Wikidata has its own literal model](https://www.mediawiki.org/wiki/Wikibase/Indexing/RDF_Dump_Format)
- Maybe future work of extending it
  - what would it mean in dataspecer
  - and the created ontology

## Testing 

### Searching classes and properties

```
Class input bar:
    [ name ], [ short description ]

Properties input bar
    [ name ], [ short description ]
     ((+) Add button)
```

- Searching concepts:
  - with what information?
      - searching without properties
        - with name
        - with description
      - searching with properties
        - how many properties
        - with name
        - with description
      - what the information consist of?
         - keywords in name
         - sentences in description
         - does the query contain entities we know of?
         - is it long/short?
- Searching properties:
  - the same as concepts

<br>

- Queries for conceps, queries for properties - isnt it too many?
  - maybe always provide the full information

Example:

```
Class input bar:
    [ Turistic attraction ], [ a place visited by tourists ]

Properties input bar
    - location = [ location ], [ a place where something is located ]
    - operator = [ operator ], [ maintainer of a thing or place ]
    - owned by = [ owner ], [ a person or organisation who owns a thing ]
     ((+) Add button)
```

- results:
  - i am not really sure how to make a list of results
  - i can image the one we want but not the rest
- **Maybe approach it differently**
  - instead of making a list of results
  - create the queries
  - let users rate the results given from the engine

### General testing of using wikidata inside dataspecer

- Maybe instead of creating queries and list of results.
- We could test it together with the general usage of the ontology inside dataspecer
  - did the user manage to find his desired class with properties?

<br>

- **What to measure?**
  - satisfaction with the data structure and the root class
  - ease of use
- **How to measure it?**
  1. Give a user a task to model a data structure based on description.
       - Preferably a user who knows data specer already?
       - Something that we know can be modeled, but maybe there is no straightforward way to do it.  
  2. The task is split into two parts
     1. searching a root class
     2. selecting the surroundings
  3. For each part
     1. device a series of sub tasks
        1. searching root class
             - use the search bar only with keywords, then with descriptions, then with assigning properties
        2. selecting the surroundings
            - finding the relevant properties in the class, then with including hierarchy
            - searching with text bar
     2. device rating questions
        1. searching root class 
            - based on class results
            - based on properties present on the class
            - ranking the results from each usage (name only, with description, with properties selected)
        2. selecting the surroundings
            - based on properties present on the class,
            - maybe the existing endpoints on associations?
            - how was it difficult to find it? search bar, including hierarchy, browsing ancestors      
   4. Overall questions for the task.

## Comments

- urovne obtiznosti
  - osa x - root 
    -  easy, root complex, root does not exists
  - osa y - surroundings 
    -  easy ( jen naklikam, ne pro does not exists)
    -  surroundings large list , napriklad surroundings s domain a range
    -  complex - traget class for selection
    -  no surroundings 
-  pro kazde dva priklady
- uvazovat ze ty veci tam jsou
uzivateli nereknu kombinaci, ale udelam konfigurace v ulohach
kazdemu evaluatorovi dame jeden typ