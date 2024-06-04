# Search initial method selection with the help of users.

- What?
  - Ask users to find a class and write queries for the class.
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
  - How will he find the classes?
    - There is only limited number of instances?
    - The user is biased from the Wikidata search engine.
- What to measure?
  - Existence and rank of the class in the results, lets say in the top 30 (the size of the page a user will see).
  - Performance of the methods.
- How to measure it?
  -  Mean reciprocal rank
     -  Because we want to look only for the first relevant results, which is our class.

<br>

- Additional questions:
  - Should we tell them what queries to write?
    - If yes it can be biases towards sentences x dense embedding or keywords with sparse/keyword search.
    - I think keeping it to the user is the best way.
  - I do not think that telling them the properties is a good idea now.
  - Maybe instead of letting the users choose classes.
    - I could randomly choose a number and then split it among test subjests.

## Ask a user to find a class and generate queries.

1. Najdete ve znalostnim grafu Wikidata alespon 3 tridy.
   - Wikidata se skladaji z entit. Kazda entita obsahuje vlastnosti (properties), ktere maji jako hodnotu literal (cislo, text) nebo entitu. Entity se dale deli na druhy: items, properties, lexemes, norms, a forms. Kazda entita ma unikatni identifikator skladajici se ze slozeniny jednoho pismena a kladneho cisla. Napriklad Q30, P31, L123. Kazdy druh entity ma prirazen jedno unikatni pismeno. Pro druh items je to pismeno "Q". Pro druh properties je to pismeno "P".
   - Trida je definovana:
     1. Kazda trida je pouze entita druhu items, tj. ma identifikator pocinajici pismenem "Q". 
     2. Entita druhu items je trida, jestlize obsahuje vlastnost "subclass of".
     3. Tridou je hodnota vlastnosti "subclass of", na kterekoliv entite.
     4. Trida je hodnota vlastnosti "instance of", na kterekoliv entite. 
   - Jak nalezt tridy:
     1. Otevri [Wikidata vyhledavac](https://www.wikidata.org/w/index.php?search=&search=&title=Special:Search&go=Go)
     2. Hledej pomoci vyhledavaciho pole:
        - Zadejte hledany vyraz a pridej vyraz "haswbstatement:P279" oddeleny mezerou.
          - Vysledky hledani obsahuji tridy.
          - Po rozklinuti tridy muzete navigovat do dalsich trid pomoci kliknuti na hodnotu vlastnosti "subclass of".     
        - Zadejte hledany vyraz a pridej vyraz "haswbstatement:P31" oddeleny mezerou.     
          - Vysledky hledani obsahuji instance.
          - Rozkliknuti instance muzete navigovat do tridy pomoci kliknuti na hodnotu vlastnosti "instance of".
2. Po nalezeni tridy si predstavte, ze danou tridu nemate, ale chteli byste ji najit. 
3. Vygenerujte alespon 5 ruznych dotazu v anglictine, ktere byste pouzili k vyhledani dane tridy.
    - Dotaz je textova hodnota, ktera ma maximalne 60 slov.
    - Dotaz muze obsahovat klicove vyrazy nebo kratky popis.
    - Napric dotazy muzete opakovat vyrazy, podminka je, aby dotaz neobsahoval kompletne stejny text, jako dotaz jiny.