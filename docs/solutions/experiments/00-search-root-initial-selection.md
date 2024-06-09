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
- Why?
  - We have many search methods, no gold data and we need to find what is the best method.
  - This will server as initial selection of methods.
  - The best methods will later be tested by users.
  - It is difficult to create a list of top K results for a query.
    - And device the queries as well.
- Problems and bias?
  - Every user sees it differently.
    - Every one can generate queries differently.
    - Maybe select classes globally and then make each user generate queries.
  - It does not reflect the variablity of the returned data.
    - It can return relevant results but this method will not find it.
  - How many classes and how many queries?
    - The user must be thorough.
      - We were thinking about 8 classes per user and 4 queries.
- What to measure?
  - Existence and rank of the class in the results, lets say in the top 30 (the size of the page a user will see).
  - Performance of the methods.
- How to measure it?
  -  Mean reciprocal rank
     -  Because we want to look only for the first relevant results, which is our class.

<br>

## A users search query generation.

Thank you for participating in the user search query generation process.

Your task will be to generate a list of textual search queries for a predefined list of classes from Wikidata.

1. Where to find the classes:
     - The list of classes is located in this public [sheets file](insert).
     - The list itself is divided into sub-lists of eight classes.
     - The sub-lists are separated by an empty line.
     - Your assigned classes are in the first sub-list, coming from the top to the bottom, that has not yet been marked as taken.
     - When you locate the sub-list, mark it as taken by filling the appropriate column on the left side of the sub-list.
     - Now, the sub-list you marked as taken contains the classes that you will be generating the search queries to.
     - In the sub-list, you will see the label of the class and a link to it's Wikidata page.
       - On the Wikidata pages you will see labels, descriptions, aliases, and additional properties in the form of statements.

2. Generating the search queries:
     1. For each class from the sub-list, generate **4** textual search queries in English language as if you wanted to find them.
        - **You can use keywords, short descriptions, full sentences, or any combination of the mentioned**.
        - **Limitations**:
          - The queries cannot be exactly the same.
          - Limit the length of the textual search query to 200 characters.
          - You are **not allowed** to use the label (the title of the page) of the class as is.
          - You are **not allowed** to use the description as is, but you are welcome to modify it and then use it. 
        - You can visualize the tasks as if you were given a search input bar, and you want to find the given class, you write the query and then press the search button. Naturally, you would expect the most relevant result to be at the top.
        - To learn more about the class, visit the provided link to it's Wikidata page.
          - Look at the aliases ("Also knows as" column), description, or statements.
     2. When you are finished, insert each of the queries to the columns on the right side of the class.







