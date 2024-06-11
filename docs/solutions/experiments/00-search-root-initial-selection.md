# Search initial method selection with the help of users.

- What?
  - Ask users to find a class and write queries for the class.
  - We have moved from asking the user how to find a task to selecting a classes that the user will write query to.
    - Since the user would be biased towards the queries he used during the search.
    - The selection was done based on the number of instances, number of children, and number of ancestors.
      - Each category should be done by all users to not conform to addditional bias.
  - When provided the users with classes, they should not see the others solutions.  
  - We wont tell them what queries to write, only not to use the label of the class.
    - If yes it can be biases towards sentences x dense embedding or keywords with sparse/keyword search.
  - We wont tell them about properties.
  - So that the users would not see the results of the other users, do not put the inputs next to each other.
- Why?
  - We have many search methods, no gold data and we need to find what is the best method.
  - This will server as initial selection of methods.
  - The best methods will later be tested by users.
  - It is difficult to create a list of top K results for a query.
    - And device the queries as well.
- What to measure?
  - Existence and rank of the class in the results, lets say in the top 30 (the size of the page a user will see).
  - Performance of the methods.
- How to measure it?
  -  Mean reciprocal rank
     -  Because we want to look only for the first relevant results, which is our class.
- Problems and bias?
  - Every user sees it differently.
    - Every one can generate queries differently.
    - Maybe select classes globally and then make each user generate queries.
  - It does not reflect the variablity of the returned data.
    - It can return relevant results but this method will not find it.
  - How many classes and how many queries?
    - The user must be thorough.
      - We were thinking about 8 classes per user and 4 queries.

<br>

## Users search query generation

Thank you for participating in the user search query generation process.

**Task**

Your task will be to generate a list of textual search queries for a predefined list of classes from Wikidata. Please, follow the task description below.

**Instructions**

1. Locate the classes:
     1. The list of classes is located in this public [sheets file](insert).
     2. Locate the first free sub-list of classes.
        - The list itself is divided into sub-lists of eight classes.
        - The sub-lists are separated by empty lines.
        - **Your assigned classes** are in the first sub-list, coming from the top to the bottom, that has not yet been marked as taken.
     3. When you locate the sub-list, **mark it as taken** by filling the appropriate column on the left side of the sub-list.
     4. Now, the sub-list you marked as taken contains the classes that you will be generating the search queries to.
2. Generate queries:
     1. For each one of the eight classes from the sub-list you marked as taken, generate **4** textual search queries in English language as if you wanted to find the particular class in a set of thousands of classes.
        - **You can use keywords, short descriptions, full sentences, or any combination of the mentioned**.
        - Use the provided link to learn more about the class.
          - Look at the aliases ("Also knows as" column), descriptions, statements, or think about it's instances.
          - It is still not enough, you can use internet.
        - **Limitations**:
          - The queries cannot be exactly the same.
          - Limit the length of the textual search query to 200 characters.
          - You are **not allowed** to use the label (the title of the page) of the class as is, but you can use synonyms and aliases. Also, you can modify or rephrase the label.
          - You are **not allowed** to use the description as is, but you can modify or rephrase it. 
3. When you are finished, insert each of the queries one by one to the columns on the right side of the class.
4. After you finish the task, please fill in the questionare below.

--------------------

Questionare questions:
  1. Characterize yourself:
       - student
       - teacher
       - modeling expert
       - database expert
       - Programmer
       - Manager
  2. I understood the meanings of the classes.
     - Fully disagree | ... | Fully agreee 
  3. I found the task of generating textual search queries difficult.
     - Fully disagree | ... | Fully agreee
  4. It took me approximately:
      Time in minutes
