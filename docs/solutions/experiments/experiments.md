# Experiments 

# 6. meeting comments

## Searching classes and properties

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

## General testing of using wikidata inside dataspecer

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

# 7. meeting

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

# 8. meeting 

### Testing

- Should we test searching of properties
- Or should we give them what properties they are looking for.

### Comments

- netestovat uzivatele
- ale dat nam dotazy
- nereflektujeme to hledani
- ale najdeme tridu
- a pak k ni dotazy a ja pak mechanicky otestuju jestli ta trida tam je
  - uzivatel nam vygeneruje dotazy jak by hledal tu tridu
    - pevnost
    - historicke misto ktere hralo roli ve valkach
- problem je ze to kazdy vidi jinak
  - ale muze to udelat blbe protoze tomu odpovidaji jine tridy
  - je to riziko te metody 
  - predtim je ze jsem spokojeny
- mozna kombinace 
  - nejdriv automatizovane a pak tri nejlepsi dat uzivatelum a reranking taky
  - vytipuju nejlepsi kombinace a chci se je seradit -> blbe to je kdyby to bylo 0,1 - 0,2
  - musime zkusit je rozdistribuovat
  - a ti kandidaty muzeme dat na detailnejsi posouzeni
  - podme najit dve tri tridy a pro kazdou z tech trid si pripravit dotazy a pak si ty dotazy pustit
    - a zmerit jak vysoko tu tridu renkovali
    - a zprumerovat pres vsechny tridy
    - a tehle 5 dame pro produkcni posouzeni
    - ale muzou fungovat dobre ale treba blbe vuci uzivatelum
  - a pro ne to pak rucne zevaluovat


# In general

- Chceme testovat dve veci
  - Root search
  - Modeling

Pro dve veci mame dve ruzne metody.

- Modelovani
  - Uzivateli dame topic a tridu kterou ma namodelovat.
  - Dame mu cas - treba 10 minut
  - Skonci
  - My to projdeme a zmerime kolik toho namodelovali.
  - Aby to bylo srovnatelne, musi delat stejne tasky.
  - Delame prumer napric tasky a napric evaluatorovi.
  - Merime:
    - Prumer kolik toho stihli namodelovat - napric tasky a testerem.
    - Spokojenost s tou praci a dialogem. 

<br>

- Root search
  - Problem je ze nemame data -> nemame dotazy a nemame vysledky.
  - Delat dotaz a pro nej list top 10 vysledku je tezke. Navic mame spoustu dotazu.
  - Jak budeme testovat?
    1. Nejdriv  udelame mechanicke testovani.
       - Uzivatel nam vybere tridu 
         - Da nam k ni dotazy, jak by ji hledal.
         - My mu rekneme - udelej to pomoci keywordu, udelej to pomoci descriptions, zkus uvest property
       - My pak pro ty dotazy vykoname
       - Merime jestli jsme nasli tu tridu a jak vysoko pripadne byla.
       - To potrebujeme zprumerovat napric metodami a napric dotazy.
       - Nejlepsi 2-3 vybereme a nechame otestovat uzivateli.
       - Problem je ze to je biased a kazdy to vidi jinak -> muze tam byt relevantni trida, ale tohle ta metoda nepozna.
    2. To nejlepsi dame zivateli.
       - Bude mit serii tasku k hledani trid.
       - Tasky se budou delit:
         - Iteration -> continually add more information.
         - Anything you want.
       - Merime jestli nasli tridu.
       - A jak jsou spokojeni.    


# Meeting with LP

- Obecne 
  - vuci cemu to porovame 
    - root search base line method with simple string matching
    - ale co ten dialog na prohledavani 
      - tam nemame protoze to neexistuje
      - sbirame pocitovy feedback od uzivatelu
      - uzivatelu se zeptame na pocitove otazky
  - between user
    - da nam mene signifikantni vysledky
  - kdyz pracoval s tim puvodnim tak je tam bias te studie - carry over studie
  - minimum je randomizace 
  - jake data chceme sbirat 
    - qvantitativni analyza - implicitni data behem toho co to dela
      - perception correlate k dotazniku
    - qvalitativni analyza dotaznik
      - primo se ptat na veci na ktere nas zajimaji
      - resque a user centric evaluation framwrok for recommenders systems 

- modelovani
  - tezke trefit obtiznost - muze se stat ze to vsichni dokonci
  - pridat mereni rychlosti
    - kdy se dokonci ten task
    - nebo rychlost jednotlivych stepu
    - rollback - neco vytvoril a vratil to zpatky, nutny feedback
  - pozor na presne vytvoreni zadani smeruji k stejnemu cili
  - jestli property jsou vyse nez ty co nepotrebuje
    - ndcg mean average precision

- Search 
  - lepsi nechat cely task
  - chceme itemu ktere potrebuje na prvnich mistech
  - jestli dokazal interagovat dostatecne dobre
    - nepotreboval interagovat s vice koreny
  - opatrnost na bias jak se ptame tech lidi
  - jaka je sance ze ty strukturovane metody se neprekryvaji
    - na to je dobre mit vizualizaci tech vystupu
  - nepretizit uzivatele
    - sanity check nechat to vyplnit potom kamarada jestli tu studii mel chut dokoncit
    - po kazde iteraci dotaznik
    - musime ty tasky napsat jednoduse a na mistech aby je neprehlidli
    - hlavni je nezahltit lidi
    - kratky cas aby dokazali vnimat
  
<br>

- merme vsechno co nas napadne a pak myslet co jsme zapomneli
  - do logy abychom to pak nemuseli hledat zpetne

<br>

- obecne otazky scale strongly agree neutral ...
- zkusit si odhadnout, pocet lidi abychom 
  - sample size estimation and power analysis
  - kolik lidi aby se projevily nejake rozdily
  - sluzby prolific

- preregistration
  - co merime a co chceme ziskat
  - dobre pro clanky


