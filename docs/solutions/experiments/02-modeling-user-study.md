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
After the root class is selected, the user models the data structure by adding surroundings of the root class, and subsequnetly the surroundings of the added classes.

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
   5. Start modeling the data structure by clicking on the `(+)` button next to the class. The button opens a surroundings dialog.
      - Select appropriate properties, click confirm.
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
  5. I consider the filter by instance useful.
  6. Information provided in the surroundings dialog was sufficient for me to select adequate properties.
  7. The surroundings dialog was sufficiently responsive.
  8.  I found the surroundings dialog intuitive to use.
  10. The surroundings dialog enabled me to accomplish the tasks.
  11. I would use the surroundings dialog again.