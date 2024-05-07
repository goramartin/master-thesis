# 7. meeting

This meeting I would like to talk about:
1. Brief overview of what I did.
2. State of research project
    - Deployment
    - Questions about handing in the project.
3. Testing

## Brief overview of what I did

- Finished up the programming part of research project.
- Documentation
- Adding scripts to Research project
- Think about what to change in project to adjust for the search engine
- Will meet with Jakub K. from Datlowe on Thursday.
- Will meet with Ladislav P. somewhen in late May. 

## State of research project 

- All programming features are done.
- Documentation
  - Lastly, missing developer documentation in Dataspecer.

<br>

- Implemented new utility scripts into preprocessing
  - Downloading with resume on error.
  - Run all phases
- Implemented Docker image for the API service 

<br>

- **Deployment**
  - Preprocessing as is.
  - Elastic assuming runs in docker.
  - API service can be run "normally" or in docker, but needs restart to load new data.
- So far no simple deployment (e.g. docker-compose)
- In Dataspecer a separate branch -> needs connection to backend.

- **Questions**
  - Should I hand in the entire repository?
    - Contains also my "personal" comments.
  - How to show it to the opponent?
    - Need to work on the diploma.
    - Cannot have the elastic/API-service running.
    - Maybe a meeting with demonstration or video?
  
## Testing 

```
Class input bar:
    [ name ], [ short description ]

Properties input bar
    [ name ], [ short description ]
     ((+) Add button)
```

- Last time we dicussed the way to test the search and data structure creation.
- Reminder
  - Do not device queries and top N results.
  - Instead create modeling tasks for users, make the users answer questions.
    - Tasks based on scenarios - easy, intermediate, complex (axis for root search and surroundings)

<br>

- Root search testing
  - A user must switch between search solutions - to review each of my solutions.
    - How?
      - Switch on the frontend?
    - And how many?
      - iterations 
        - search only with keywords, then add descriptions , then add with assigning properties
        - for each step collect feedback
      - or just use everything 
        - assigning properties, description, name...
        - collect feedback for the entire part
      - or just use anything you want
  
## Comments

- pro root search separatni reseni - neresit modeling
  - iterace + anything you want (pro kazdou kombinaci), tehle 8 uloh musi byt slozitosti stejne a 8 uloh slozitostne, ve smyslu clarity pro uzivatele
  - complexnost - 16 uloh, do 1-2 hodiny zvladnutelne by to melo byt zvladnutelne,
  - nechat  ho udelat vsechny
  - musim zjistit na co se ptat uzivatele a jake ty metriky pouzit
  - a predstavit mu ty ulohy, a pak se s nim pobavit i o tom modelovani

- pro modelovani
  - si jak dlouho modelujes
  - jestli se to podarilo namodelovat
  - tam ten feedback nemusi byt takovy
  - modeluj maximalne 10 minut
  - co tam bude to tam nech
  - my dva to projdeme a budeme to srovnavat
  - a zhodnotime kolik se tomu podarilo namodelovat
  - kolik procent se podarilo namodelovat uzivateli
  - prumer napric ulohava a napric evaluatorovi
  - aby to bylo srovnatelne, musi delat stejne tasky
  - a mozna to nevazal na root search, ale uz ten koren ma byt vybrany
  - a pak zacni modelovat a za 10 minut odejdi,
  - 2 complex (nested) a 2 easy (flat) a nechameto nechat