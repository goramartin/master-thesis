# The modeling user study

- What?
  - A user is given four modeling tasks.
    - The tasks are devided into 2 groups.
      1. A flat modeling - 2 tasks, intuitively, this is easier that the other.
      2. A composite modeling - 2 tasks.
    - The tasks have a given root class. 
    - For each task, the user is given at most 10 minutes.
  - All users do the same modeling tasks.
  - After the 10 minutes, we look into the results of the modeling task.
- Why?
  - We created a dialog for Wikidata into the Dataspecer tool.
  - We want to test whether the dialog is usable and "enough" for modeling tasks.
- What to measure?
  - Were the properties on classes reasonable?
  - How much of the task was completed.
  - Ease of use
  - It helped him to accomplish the task.
  - Whether the interface was adequate
  - Whether there was enough information to complete the task.
  - Overall satisfaction
  - I would use it again.
- How to measure it?
  - Questionare questions 
- Problems and bias?
  - Every user sees it differently.
    - Every one can generate queries differently.
  - How many tasks?
    - The user must be thorough.
    - At least 4.
  - The problem might be the task difficulty.
  - We must create tasks that lead to the same result.
- Collecting additional metrics?
  - Not sure what.

## The modeling user study

Thank you for participating in the modeling user study.

**Introduction**

[The Dataspecer tool](https://dataspecer.com/) enables users to model a tree-like data structure based on an input ontology.
The data structure can be used to generate various software artifacts.
The ontology is a set of classes and properties. 
The properties are divided into attributes and associations.
To create the data structure, one must start by searching for an appropriate root class of the data structure.
After the root class is selected, the user models the data structure by adding properties of the root class to the data structure.
The data structure is further modeled by adding properties of the already added property endpoints.  

**Task**

Your task is to model four data structures based on the domain descriptions listed below. There are four domain descriptions. For each description, you will create one data structure. Please, follow the instructions below.

**Instructions**

1. Create a data specification in the Dataspecer tool.
     1. Open this [link]().
     2. Click on the "Create specification" button, enter label "modeling_testing".
     3. In the "Vocabulary sources" select Wikidata and click on the button "save".
2. Iterate over the domain descriptions listed below from top to bottom and do:
   1. At the top the data specification page, click on the "Create data structure" button.
   2. At the top right corner, click on the "Set root element".
   3. Into the input box, copy the IRI of the root class.
   4. Select the class by clicking on it.
   5. Start modeling the data structure by clicking on the `(+)` button next to the class name. The button opens a surroundings dialog.
      - Select appropriate properties, then click confirm.
      - Repeat on the added properties until you are satisfied. 
      - Model the domain for 10 minutes maximum.
      - [A guide how to use the dialogs]()
   6. When you are finished or the time expires, click on the button "Back to specification manager" in the right upper corner.
3. After you finish all the modeling tasks, fill in the questionare below.

**Domain descriptions**:

1. X
   - Root class:  
2. X
   - Root class: 
3. X
   - Root class: 
4. X
   - Root class: 

-------------

**Questionare:**
  1. Characterize yourself:
     - student
     - teacher
     - modeling expert
     - database expert
     - Programmer
     - Manager
  2. I understood the modeling tasks clearly.
       - Maybe for each modeling task?
  3. I managed to complete the tasks in the time limit.
        - Maybe for each modeling task? 
  4. I found it easy to understand the meaning of the classes and properties in the surroundings dialog.
  5. Information provided in the surroundings dialog was sufficient for me to select adequate properties.
  6. The surroundings dialog was sufficiently responsive.
  7.  I found the surroundings dialog intuitive to use.
  8.  The surroundings dialog enabled me to accomplish the tasks.
  9.  I would use the surroundings dialog again.
  

## The modeling tasks

### Flat modeling

- Country
  - Properties
    - flag image
    - population
    - area
    - nominal GDP
    - official name
    - capital -> capital city
      - population 
      - official name
    - head of government -> Human
      - start time
      - end time
      - birth name
      - member of -> political party
        - member count
        - name 
    - currency -> currency
    - langauge used -> modern language
  - Description
    - Model a data structure for exchanging general information about world countries. The data will be used to form a small information panel. The data structure should contain the number of people living in the country, the overall size, a name, nominal GDP, and GDP at purchasing power parity of the country. Each country has a capital city with a total population and a name. The information panel will also contain a current head of state with a name and time of election to office. The head of state also pertains to a political party. The panel must contain the name of the party and the overall number of members. Lastly, the panel will contain information about the official language and currency.
  - Link
    - http://www.wikidata.org/entity/Q6256

<br>

- A touristic attraction
  - Properties:
    -  Disabled accessibility -> quality
    -  Link to a official website
    -  Owned by -> human
       -  telephone
       -  email
    -  Operator -> organization
       -  tepephone
       -  email
    -  The maximum number of people allowed into the attraction.
    -  A language used -> language
    -  Opening time -> time
    -  Opening days -> days of the week
    -  Full address 
    -  A country -> country
    -  Coordinate location
  - Description:
    - Model a data structure for representing tourist attractions on Google Maps. The data structure should contain information about the official website, opening times, and attraction entry fees. Additionally, there is the need to include an organization that operates the place and a person that owns it. Each attraction has a limit of tourists available to entry, a language available at the site, and information about accessibility for disabled people. The tourist attraction has a complete address with a country and its coordinated location on the map. Lastly, we need the owner's and operator's email addresses and telephone numbers.
  - Link:
    - http://www.wikidata.org/entity/Q570116

<br>

### More in depth modeling

- A scholarly article
  - Properties
    - Title
    - Publication name
    - DOI
    - Main subject to genes
        - Genomic end
        - Genomic start
        - Genomic association -> Rare disease
          - Symptoms and signs -> Symptoms and signs
            - name
            - SNOMED ID
          - name
          - SNOMED ID
        - Encodes -> protein
        - Chromosome -> chromosone
    - Works that cite this article <- article 
      - DOI identifier
    - Works that are cited by this article -> article
      - DOI identifier
    - Published in -> journal
        - Name
        - Official website
  - Description
    - Model a data structure for applications exchanging data about scholarly articles specialized in genes that cause rare diseases. The data structure should have a title, a publication date, and a DOI identifier. Subsequently, the journal where the article was published should be present with its name and official website. The scholarly article is also described by the articles it is cited by and the articles it cites. The citation articles only contain DOI identifiers. Lastly, the scholarly article includes a description of the main subject, genes. The genes should contain a genomic end, a genomic start, and an HGNC identifier. The genes are also associated with a rare disease, the protein they encode, and the containing chromosome. For rare diseases, we need a name, a SNOMED disease ID, and a list of symptoms with a name and a reference to SNOMED symptom identifiers. 
  - Link
    - http://www.wikidata.org/entity/Q13442814

<br>

- Album
  - Properties:
    - Publication date
    - Title
    - Number of parts of this work
    - Review score
    - Spotify album id
    - Performer -> musical group 
      - Inception
      - Name
      - Members count
      - Spotify artist id 
      - Member of <- human
        - Birth name
        - Pseudonym
        - Country of citizen ship -> country
        - Time of join
      - Has parts -> songs
        - Duration
        - Title
        - Audio
        - Video
        - Lyrics by -> human
          - Birth name
          - Country of citizen ship
      - genre -> Music genre
        - Label
        - Url
  - Description:
    - Model a data structure for exchanging data about musical albums for a new audio player application. An album is characterized by the date it was published, a title, a reference to a Spotify album, and the number of songs it contains. Additionally, users' reviews must be included to enable relevant ordering. The album is associated with the musical group that performs the song, a genre of music, and a list of songs. Each song has a duration, title, and appropriate audio and video files. Each song also includes a writer of lyrics, denoted by its name and country of origin. The musical group encompasses inception time, the name of the group, a reference to a Spotify artist, and a number of members. The musical group has members represented by their pseudonym, the time the member joined the group, a name, and, again, country of origin. Lastly, the genre will be displayed only with its name and a link to additional information.
  - Link:
    - http://www.wikidata.org/entity/Q482994

