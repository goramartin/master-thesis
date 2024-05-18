# Expansion with the llm

- I am not going to implement this - since it got really fast complicated.

- Based on the user input:

    Concept input:
    [ name ] [ description ]
    
    Properties input:

    [ name ] [ description ]
    [ name ] [ description ]

    (Topic selection either implicit or explicit)


- What to expand?
  1. Finding a name for a concept?
     - based on the description needed 
  2. Finding a description for a concept?
     - based on the concept name
     - either needed to prompt the use again to select the concept 
  3. Finding a name for a property?
     - the same as before 
  4. Finding a description for a property?
     - prompt needed again 
  5. Additional information that is stored in the concepts?
    - that would need a specific information in the concept fields
    - or already the llm knowing what the thing is
    - What?
      - characteristics
      - synonyms 
      - ...
  6. Properties for a concept if there are none?
     - I would do it just for the string and would not add them the same importance as the user input fields
     - propbably maybe just for the properties for this type or adding the most used properties
     - that would help in the lexicalization 
  7. a topic regarding the thing
     1. implicit 
        - ask the llm to assign it a topic from a given set
        - or compute it with the precomputed topic vectors - similarity cos
     2. explicit
        - nothing would be expanded