# Search root user study.

- What?
  - A user is given a list of tasks modeling tasks and method to test.
  - The tasks will be semi iterative.
    - First, without the filters, then with the filters.
  - The tasks should not be long, there should be some easier and harder tasks.  
  - Execution:
    - A user does the tasks for only one method, the tasks are the same for the both methods.
    - For each task at most 5 minutes.
- Why?
  - We have chosen a 2 methods that provided a good performance from the previous methods.
  - We need to determine whether the methods provide a meaningful results from the users' point of view.
    - Because determining the better method from two might be difficult.
- What to measure?
  - Since we want to test the groups of users, we need to come up with a metric that would enable us compare the results.
    - We can compare the number of users who found a good class - meaning they could fullfill the requirements.
    - Or we can collect the queries and then do a third round of collectively deciding what is the better method.
  - In general for the methods:
    - Perceived accuracy:
      - Whether the methods found a good class - and also what class and possibly rank.
      - Whether the results overall were relevant.
      - Whether the Properties helped the search.
      - Whether the boost helped the search.
    - Ease of use:
      - Whether they found the interface intuitive
- How to measure it?
  - Questionare questions 
- Problems and bias?
  - Every user sees it differently.
    - Every one can generate queries differently.
  - How many tasks?
    - The user must be thorough.
    - At least 4, the same for both methods.
  - What methods?
    - Iterative vs Free
      - I believe the free would be better for the user.
      - Instead of forcing to use keywords/sentences, the text input should be free.
      - The force would be in a diffrerent direction
    - Instead of doing Iterative vs Free, we can do semi free
      - The text input will be free
      - But then we ask him about use only text input, then with properties.
      - We could maybe leave the boost as is and do not force him to use it.
        - It depends on the class we choose, since it can deteriorate the search if the task is focusing on not a well known class.
  - Should a user do all the tasks on one method or should he do randomized methods on both methods.
  - Two possibilities of execution:
      1. User does the tasks on only one method, the tasks are the same for the both methods and the order does not need to be randomized.
         - Users need to be split among the groups.
         - We have a same list of tasks for both methods.
      2. A user uses both methods but with different tasks.
         - We bring bias on the tasks - what if the tasks for one group are easier than for the other method?
         - The minimum is to randomize the tasks, but it is difficult for the user.
         - A user might learn to use the search before moving to the other method.
- Collecting additional metrics:
  - Queries used
  - Clicks on class selection
  - Clicks on the class detail.

<br>

Additional questions:
 1. How to split the form into two groups.
 2. Asking about the property filter or boosting.


## Search root user study

Thank you for participating in the user study.

**Introduction**

[The Dataspecer tool](https://dataspecer.com/) enables users to model a tree-like data structures based on an input ontology.
The data structure can be used to generate various software artifacts.
The ontology is a set of classes and properties. 
To create the data structure, one must start by searching for an appropriate root class of the data structure.
After the root class is selected, the user models the data structure by adding properties of the root class to the data structure.
The data structure is further modeled by adding properties of the already added property endpoints.  

**Task**

You are assigned four data structure descriptions listed as part of the questionnaire. For each description, you are tasked to search for an appropriate root class of the data structure in the Wikidata ontology using the Dataspecer tool. **Your task is to only find the root class. Do not model the entire data structure.**

**Instructions**

1. Open the search dialog in the Dataspecer tool:
     1. Open this [link]().
     2. Click on the "Create specification" button, enter any label you want and then click create.
     3. In the "Vocabulary sources" select Wikidata and click on the button "save".
     4. Proceed by clicking on the large rectangle "Create data structure" button at the top of the page.
     5. Click the "Set root element".
     6. **In the top side of the panel select the method X.**
     7. You have successfully opened the search dialog.
2. The questionnaire below contains the four data structure descriptions. Fill in the root search tasks questions. 
   - During the search, please, try paying attention to the result lists and their relevance to your queries. You will need to answer a question about relevance in the questionnaire.
3. When you are finished with the tasks. Fill in the rest of the questions.

**The search dialog tips**

  - By clicking on a class in the search dialog, the class will be selected as a root class.
  - By clicking outside of the dialog, the dialog closes. Then you can simply reopen it and select again the **method X**.
  - In the search dialog, you can:
    1. Input keywords, a short description, full sentences or any combination of the mentioned into the text input box.
    2. Use the properties filter that enables you to select properties the class must have.
    3. Use the widely used classes boost option that enables you to give more relevance to classes with many instances.
    4. View a detail of the class, by clicking on the `(i)` icon and navigating to a "Wikidata" panel.
       - There you can navigate to the "Wikidata" panel and see properties, ancestors, and external ontology mappings of the class.
       - You can also browse the Wikidata link (the arrow next to it's name) to learn more about the class. 

---------------

**Questionare**:
 1. Characterize yourself:
       - student
       - teacher
       - modeling expert
       - database expert
       - Programmer
       - Manager
 2. Domain description here
    - Search for the root class you would use to build the described data structure. Try both with and without the property filter and boosting. Give yourself 5 minutes at most.
    - Questions:
        - I understood the data structure description clearly.
        - Did you find a root class?
            -  did not find ... found perfect class
        - Insert it's name and an identifier (located next to it's name in parenthesis). 
        - ? Using the property filter helped me to find the right class.
        - ? Using the boosting of widely used classes helped me to find the right class.

1. General questions
    1. The search engine returned relevant results to the provided queries.
    2. I found the most relevant results at the top of the result's list.
    3. I consider the property filter useful.
    4. I consider the boosting of widely used classes useful.
    5. The information provided was sufficient for me to select an appropriate root class.
    6. The search engine was sufficiently responsive.
    7. I found the search engine intuitive to use. 
    8. The search engine enabled me to accomplish the tasks.
    9. I would you the search engine again.
  
## Tasks

1. A bunker
   - Link
     - http://www.wikidata.org/entity/Q91122
   - Properties
     - service entry
     - service retirement
     - maximum capacity
     - floors below ground
     - schematic
     - state of conservation -> conservation state
     - significant events -> battle 
     - conflicts -> world war
   - Description
     - Find the root of a data structure for exchanging data about defensive military buildings designed to protect people and materials from enemy attacks. The buildings were extensively used during World War I-II and usually contained many floors below ground. The data will be used to display information panels in a war museum. The root needs to represent information about conflicts and significant battles the building participated in. Information about the building's schema, capacity, and time it entered and retired service must also be included. Lastly, the panel must state the current state of conservation.

<br>

2. A co-educational school
  - Link
    - http://www.wikidata.org/entity/Q67383935
  - Properties
    - students count
    - name
    - teaching methods
    - curriculum topics
    - educated at
  - Description
    - Find the root class of a data structure for exchanging data about schools/universities that enable enrollment of both male and female students. The data will form an online brochure for educational institutes' fairs. The root class needs to be associated with famous people who were educated at the institute, the number of current students, a name, and methods used for teaching. Topics/subjects included in the curriculum must also be present. 
  
<br>

1. A type of chemical entity
   - Link
     - https://www.wikidata.org/wiki/Q113145171
   - Properties
     - chemical formula
     - chemical structure
     - mass
     - has effect
     - InCHl
     - interacts with
   - Description
     - Find the root class of a data structure for exchanging data about general chemical substances and entities. The class must be general enough to encompass all objects of interest in chemistry. The most important properties are the description of the chemical formula accompanied by a chemical structure and the weight of the chemical object. Additionally, the class must provide properties for the effects of the objects, an international chemical identifier (InChl), and a list of other objects it interacts with.

<br>

4. A municipality of Luxembourg
   - Link
     - http://www.wikidata.org/entity/Q2919801
   - Properties
     - unemployment rate
     - number of households
     - average income
     - poverty incidence
     - population
     - electoral district
     - cadastral district
   - Description
     - Find the root class of a data structure for exchanging data about administrative territorial entities that provide municipal services in Luxembourg. The data will be provided for Luxembourg's Open Data Catalogue. The root class must provide a name and statistical information about the entities. The class should represent the population, the unemployment rate, the number of households, the average income, and the incidence of poverty. Furthermore, an associated electoral and cadastral district must be present.