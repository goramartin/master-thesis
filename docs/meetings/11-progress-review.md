# 8. meeting

1. What I did.
2. Report on the search query generation user "study".
   - Form results
3. Testing the queries from the study.
   - User x "Mechanic" queries
   - Results
   - Choosing the two methods  
4. Root search user study tasks overview
5. Diploma?

## Brief overview of what I did

- Spend a day on finding the lost random generator seed.
- Finished writing the Root search tasks for out user study.
- Collected queries from users from the previous user study.
- Created additional queries from labels and descriptions.
- Executed queries for all methods.
- Analysis of the search results.
- Choosing two methods for user testing.
- Integrated into the Dataspecer.

## Report on the search query generation user "study"

- Collected results from 15 people, but we can use only the 14 people results.
- Most people understood the meaning of the classes in general.
- People noted it was difficult to generate the queries:
  - Difficult for either too specific or too general.
  - We have updated the list of classes to be more "common knowledge" but still some classes prooved to be difficult for some users.
- 60% used AI
- On average the time it took was ~ 1 h, with exception max of 1h 45m  or 15m 

## Testing the queries from the study

### Queries

- Types:
  - User queries
  - Mechanic queries - labels with description since they were not allowed to be used as they are.
    - Label only
    - Description only
    - Label with description only
    - Label with user queries
- Overall 1507 queries.
- No aliases since people could use them directly.

### Methods

- Single methods 
  - only one method no reranking (3 methods)
    - elastic_bm25, qdrant_sparse, qdrant_dense
  - No elastic_bm25_fielded since it cannot use fuzzy search
- Tuple fusion 
  - only two methods no reranking
  - Comninations of 2 from single methods
  - For each combination tested weight rations (27 combinations)
    - 0.1 ... 0.9
    - 0.9 ... 0.1
- Triple fusion 
  - all three together no reranking
  - All weight triple combination (36 combinations)

<br>

- For each method above we tested reranking with boosting on classes with many instances.
  - Weight rations:
    - 0.25, 0.5, 0.75

<br>

- After that choosing the best candidate selection methods
  - From the 56 combinations
  - Choosing the only best one from the fusion
  - We get 5 methods
- The 5 methods then are tested with:
  - No boost but reranking top 30 with cross encoder
  - With boost and reranking top 30 with cross encoder
- Why?
  - Since the cross encoder takes a lot of time to be tested on all of the 56 combinations + multiplied with the boosting.

### Results

- Overall the fusions are the best
- But there is not a best bethod.
- The differences are minor overall.
  - Difficutl to choose
  - A metric to look at the overall score if we pick only best match for a class from users
    - "The user was able to find the class and use it for modeling"
    - For each method we get the number of times the user could find the class.
  - Decided to pick the two methods
    - best for tuple fusion
    - best for triple fusion
    - since they are the best overall and based on found classes

<br>

- The boost works as it improves overall the results

<br>

- Cross encoder
  - In general it improves the results, but there is no marcant difference in the scores for the best methods from no reranking
  - Also it seems it dimishes the power of reranking with the boost
  - Also it is 7.6 slower than using methods without it.
  - Decided not to include it to the methods.

## Root search task overview

- Look into the methods.
- Show form.

## Diploma

- Where to write and share.
- How to structure the diploma with the research project
  - Nemusi to byt nutne oddelene
  - Soustredit se na to co uz mam v nejakych pozdejsich kapitolach
  - Jen na konci rict co uz vlastne je ten prispevek a co je noveho
- Level of formalism on Wikidata and Dataspecer.

```
- intro
  - velice rychle dataspecer, concpetualni modely, muzeme vyuzit to co uz mame - wikidata
  - modelovani je tezke kdyz se dela rucne
  - musime rozlisit konceptualni model ve dvou situacich
    - chci popsat jednu svoji domenu v enterprise domene, nezbyva nez modelovat rucne
    - nebo vytvarit model pro komunikaci pro vymenu dat v prostredi a tam si nemuzu moc vymyslet specifika, nejake spolecne a chceme to prevzit od nekud
      - to spolecne uz je namodelovane
      - i v tom extremu muzu nekde odnekud prevzit
    - cim vic jsme v heterogennim postredi tim vic chceme pouzit to co uz je namodelovano 
  - neni to jednoduche - nevime co je ontologie a je velka
  - umoznime dataspeceru brat conceptualni model z wikidat
  - analyzujeme co to znamena, naprogramujeme extension a otestujeme
  - rekneme ze navazuje na softwarovy projekt
- dataspecer intro
  - uzivalteske hledisko
  - conceptualni modely - cim, pim, psm
  - z analyzovat vnitrni architekturu, ze mame adaptery jak to
  - a ten vstup chceme brat jako wikidata - novy adapter
- information retrieval intro
  - jak jsme videli wikidata jsou velke - chceme cislo, pocet trid bez vetsiho detailu
  - chceme metody IR
  - chceme konkretni metody ktere vyuzijeme
- wikidata analysis
  - do detailu v jake strukture jsou ty ontologie zakodovane a velikost
  - do hlounku z jake pohopim ze prijdu k wikidatum a ze nemam tu ontologii jen tak
  - co znamena tu ontologii z toho dostat
  - je mozne se dotazovat na verejna api a rict proc se to neda pouzit
  - konstatovat - tu ontologii musime identifikovat, preprocesovat, indexovat
- requirements analysis
  - analysis of requirements on dataspecer extension
  - funkcni pozadavky
    - nasepta mi to koren na zaklade tridy, na zaklade propert, filtrovani
  - kvalitativni pozadavky
    - musime zvladnou objem ve wikidatech
    - opakovani preprocesingu
  - pozadavky na vysledny conceptualni model
    - co chceme za model a namapovat ho na strukturu ve wikidatech
      - co si z nich beru a do ceho to transformujeme
- design solutions
  - achitecture
  - design soluto
  - solutions in depth and why
- implementation
  - pruvodce pro programatora
    - orientace
    - kam sahnout kdyz chceme neco upravit
- evaluace 
  - co pripravujeme
  - user 
- related work
- conclusion
  - ze jsme to rozsirili vyzkumny projekt vs diplomka
  - + future work, open questions
```