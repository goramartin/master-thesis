# User input


I was thinking multiple options:
- Paragrapm of text
- Concept with properties free text input fields
- Concept with properties with constructed query


## Paragrapm of the text

    Text input:

    Concept representing a place visited by tourists. The concept has associations: opening hours, locations...

- A paragraph
- needed extraction and linking
- probably would need to use the llm
- the most general solution
- would need entity named extraction followed by entity linking
- But I can do it with structural query below
- This would save me struggling with the extraction

## Concept with properties free text input fields

    Concept input:

    A place visited by tourists.

    Properties input:

    Opening hours
    Location

- This would mitigate the extraction of entities from the text.
- And leave it just for the matching.

## Concept with properties with constructed query

    Concept input:
    [ name ] [ description ]
    
    Properties input:

    [ name ] [ description ]
    [ name ] [ description ]

- This would help me distinguish between name and the description and would generally be easier to do query expansion for other parts
- I like this the most.

### For properties search as you type

- How would that be?
  - there is not so many properties as a user would type he would be prompted with a dialog to search properties and he would select a specific one
  - for full text easy
  - for vector search more complicates - can take some time before lexicalizing and query expansion?
  - would be okey for the user?
    - wouldnt it be annoying?
    - wouldnt be better to leave it just on some selection of the top similar
      - what would that be for a string similarity

### Input for selecting cathegories?

- There could be a radio buttons for selecting which parts should be used.
- Why?
  - to limit the concept search entities
  - better filter

    Select cathegories:
    - organisation
    - science
    - gene
    - proteins
    - human
    - movies
    - music
    - history
    - ...

A user could either choose few or the assignment would be done based on its query.