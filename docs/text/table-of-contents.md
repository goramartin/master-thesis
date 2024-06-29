 
# Searching classes in Wikidata ontology

## intro
- motivation od dataspecer from stepan
  - komunikace mezi systemy vede na ruzna schemata
  - delat to rucne je tezke, ruzna pravidla a dorozumeni
  - co vlastne dela dataspecer 
    - tvorime datove specifikace a datove struktury, ktere neasledne tvori schemata/ software artifacts
    - na zaklade concpetualniho levelu (stepan rika ze conceptual level je to stejne co ontologie) staci neformalne
      - pouzivame ji protoze all thing we may need to deploy are described in the ontology - ensuring consistency
      - musime rozlisit konceptualni model ve dvou situacich
        - chci popsat jednu svoji domenu v enterprise domene, nezbyva nez modelovat rucne
        - nebo vytvarit model pro komunikaci pro vymenu dat v prostredi a tam si nemuzu moc vymyslet specifika, nejake spolecne a chceme to prevzit od nekud
          - to spolecne uz je namodelovane
          - i v tom extremu muzu nekde odnekud prevzit
        - cim vic jsme v heterogennim postredi tim vic chceme pouzit to co uz je namodelovano 
- Prijdou Wikidata
  - Abych mohli tvorit ty specifikace a schemata, potrebujeme ty ontologie/conceptualni modely
  - Mit ty ontologie je tezke protoze je nekdo musi namodelovat, udrzovat, upravovat a poskytovat, muzou se menit
  - Jeden takovy zdroj jsou Wikidata
    - jsou free, comminuty, updating, ... (to co v projektu)
    - je tam ten poroject, ale neni to jednoduche
  - Chteli bychom mit ontologii na zaklade wikidat a mit moznost ji pouzit v prostredi dataspeceru.
  - V predchozim softwarovem projektu jsme vytvorili ontologii na zaklade Wikidat, kterou jsme castecne integrovali do dataspeceru, vytvorili jsme rozhrani, upravili pravidla atd...
  - mame nejaky zaklad, ktery je nutny rozsirit
  - dostali jsme nejakou ontologii, hrube veci co mame, cislo poctu trid
  - Posledni cast kterou je nutne vyresit je jak v takovem mnostvi vyhledavat tridy, musime analyzovat navrhnout metody, a evalutovat
  - analyzujeme co to znamena, naprogramujeme extension.
  - V teto praci take uvadime analysis and description of the previously Created Wikidata ontology and it's integration.
- pridat popis zadani jako v bakalarce
  - chceme vyhledavat tridy
    - dialog
    - metody vyhledavani evaluace
    - evaluace modelovani
    - integrace do dataspeceru

## dataspecer intro do hloubky ted uz vice technicky

- co to je datapecer a na co se pouziva
  - opacko z intra trochu vic podrobneji
  - nezminovat nic o te nase ontologii a integraci
- uzivatelske hledisko
  - uzivatel vybira vstupni ontologii
  - dela nejake datove specifikace
  - uvnitr specifikace mame datove struktury
  - popis tvorby datove struktury
    - uzivalteske hledisko a modelovani vic do hloubky nez v tom intru
    - obrazky, vystupy
- z analyzovat vnitrni architekturu a model
  - conceptualni modely 
    - cim, pim, psm
    - jak ten model vlastne vypada
    - abychom vedeli co se tam deje a pak to popsat z pohledu uzivatele
    - mozna mapovani na ten pim protoze je dulezity
  - pohleda na vnitrek
  - je tam vic aplikaci
  - services
  - packages
  - zajima nas v pakcaged adapter a hlavne editor aplikace 
  - a ten vstup chceme bereme jako wikidata - novy adapter

## information retrieval intro

- ale pak co vlastne tam potrebujeme
  - chceme metody IR
  - chceme konkretni metody ktere vyuzijeme
  - rikame ze to je velky field, ale vybirame jen veci ktere budeme potrebovat
- obecne architecture of retrieval
  - ze nektere metody jsou pomale
  - proto mame dva stepy
  - reranking
  - chceme nejaky relevance x similarity
- zakladni veci basic text matching - sparse , na zaklade tech veci ze skopalovy prednasky
  - [pouzit tohle jako reference](https://arxiv.org/pdf/2211.14876) pro postup a taky [tohle](https://arxiv.org/pdf/2403.00784)
  - vector space model
    - bag of words
    - tf idf
  - probabilistic model 
    - bm25 and bm25fielded
  - exact matching a problemy
  - fuzzy matching - levenstein distance
  - partial matching
  - analyzers - english, stop words, tokenizers ...
  - problems that the text matching cannot solve - semantic similarity
- language models - dense
  - latent semantic indexing jako history
  - ze pracujeme hlavne s dense embeddingy
    - mozna co je to training loss, vstupy a vystupy
      - co to znamena
      - input tokenizer
      - vystup
        - normalizace
        - qunatized models
    - ze byly predtim glove, word2vec...
    - transformers
      - do te doby reccurentni site
      - basic architecture - encoder, decoder - attention is all you need
        - ze umime naucit kontext slov jak z leva tak z prava.
        - chat gpt vs encoders like BERT
      - BERT
        - pretrained language model
        - can be finetuned
        - optimezed for Masked language recognition
        - and next sentence  
        - na co je a jake ma problemy
      - Sentence bert
        - nastupce bert, optimized for sentence similarity
      - Basic architectures
        - bi-encoder vs cross encoder
          - we need precomputed embeddings, otherwise too slow
        - ze bert neni dobry na bi encoder, ale cross encoder
          - je optimized na two sentences
          - protoze pridava ten layer na classification [0,1]
        - sentence bert je pak na bi encoder
          - kvuli scalabilite, jeho prednost je ze bere dve veci a porovnava je vuci sobe
          - to se neda pouzit v pripade ze mame velky dataset
          - proto mame sentence bert, ktery je fine tuned na similarity
          - vytvari embeddingy pro celou vetu
  - Sparse learned embeddings
    - jen kratky uvod
    - ze pouzivame neco jako bert, a pak koukame na distribuci slow v tech vecech, ktere se nejvic hodi pro ty slova co uz mame
    - dela to text expansion takze to zachyti vice veci
- Indexing the embeddings 
    - knn and ann
    - hnsw index
    - inverted index for words
    - filtering?
      - post, pre, during
      - hash maps
- taky zminit ze jsou dalsi veci - jako, machine learning (learning to rank), a ty starsi modely, taky ze tam jsou varianty jako poly encoder (colbert, ale ze to bere hodne pameti, a ze zatim neni moc znam)


## The Wikidata ontology 

- pipisujeme ontologii kterou jsme vytvorili ve vyzkumnem projektu
- povidame o ni jako o konecnem produktu
  - do detailu v jake strukture jsou ty ontologie zakodovane a velikost
    - nejaky basic model - to co jsem kreslil na schuzce, mozna odkazy, json atd...
    - pravidla ktera jsou, a ktera jsme pridali
    - odkazy na ten project about ontologies
    - properties prirazeni
    - do hloubky z jake pohopim ze prijdu k wikidatum a ze nemam tu ontologii jen tak
- co znamena tu ontologii z toho dostat
  - preprocessing z projekty
  - konstatovat - tu ontologii musime identifikovat, preprocesovat, indexovat
- co z toho vyjde jako vysledek
  - summary te ontologie
  - rict ze tam jsou veci ktere uplne nejdou v dataspeceru
  - nejaka basic analysis z tech mych summaries, kolik trid, kolik propert, kolik je tam class instances, ...

## State of integration 

- puvodni requiremets - rict ze jsou
  - funkci
    - on ceptual model mapping to the PIM
      - pouzit stepanum formalni popis pimu a cimu jako funkcni mapovani
    - Uzivatel bude moc pouzit vstupni ontologii na vstupu pro tvorbu datovych struktur
      - rozebrat vstup, services atd...
  - kvalitativni
    - jde to spousted znovu
    - jede to dostatecne rychle
      - pohled na backend and frontend
- Architecture overview and simple implementation
- A pak postupne prochazet requirements a rikat jak jsou splneny + nejaky background info
  - nejdelsi asi bude to mapovani na PIM od stepana, nejak torchu formalneji
    - ale vicemene mame jen tridy, properties (associace, attributy) a ty maji domain and range
- Pak rict co vlastne potrebujeme dal - udelat vyhledavani

## Requirements analysis on the search extension

- ze uz tam nejake basic vyhledavani je
    - proc nemuzeme pouzit verejna api
- co se musi rozsirit, a jak aby se nerozbil ten zbytek puvodnich requirements  
  - tj. nejaky backwards compatibility with the existing integration
- funkcni pozadavky z hlediska vyhledavani
  - nasepta mi to koren na zaklade popisu tridy
  - filtrovani na zaklade properties - ze to ma byt AND
  - moznost uprednostnit velmi zname veci
- kvalitativni pozadavky z hlediska vyhledavani
  - musime zvladnou objem ve wikidatech
  - opakovani preprocesingu, predvypocet, zavisi na tom predchozim
  - ma to byt dostatecne rychle

## Search solutions design

- picking the search solutions, abstract and not dependent on technicalities
- how and what is a good
  - intermezzo about the ontology search and importance
    - structural importance
- we do not want to train our own models
- choosing the general architecture of the search
  - multi stage retrieval
- analysis of the wikidata classes - eg. repetitions, etc... maybe enough to mention it from the wikidata ontology intro
- based on the papers
  - candidate selectors
    - single
      - maybe there is a need to be more specific when it comes to elastic
      - for each method also provide analysis what it needs
      - how to create the solutions, the documents for text search, lexicalization, expanding the names 
    - interpolation and hybrid search
      - tuple fusion
      - triple fusion
  - reranking
    - cross encoder
    - boosting based on the structure of the ontology 
      - how is it done
      - parameters, already needs to know the internal structure of the ontology
  - filtering with properties 
    - using precomputed properties for each class is a memory intensive
    - from the analysis of the classes we noted that the properties are defined somewhere in the upper ontology
    - filtering classes based on properties via filtering classes based on ancestors defining the properties
- general parameters of the search
  - max results
  - combinations

## Implementation 

  - architecture of the services
    - where runs what
  - designing a front end of the search
  - v cem to je napsane
  -  jake databaze?
  - pruvodce pro programatora
    - mame uz dokumentaci na githubu
  - uzivatelska dokumentace?
    - obrazky
  
## Evaluation

- potrebujeme evaluovat nase reseni
  - nemame data -> odkazy na nejake veci co uz mam, ale ze nic neni na nasi domenu, taky paper od pana skody
  - potrebujeme nejak urcit, ktera reseni jsou schopna vyhledavat tridy
  - vybrat nejake konkretni na pouzi lidmi
  - taky evaluovat zda se ontologie da pouzit k modelovani
- nemame data tak udelame user dotazniky
  - query generation
    - vsechno o nem z mych poznamek
    - analysis of results
      - z mych poznamek ipynb
  - user findings in integration
    - results
    - odkazy na paper od pesky + co vlastne evaluujeme
  - modeling user study
    - results
   
## Related work

- vsechno co mam od paperu
- hlavne ontology search a class importance, entity linking and rag.
- z pohledu hledani je to obecne vsechno co mame z retrievalu
- taky nutnost zminit YAGO

## conclusion

- ze jsme to rozsirili vyzkumny projekt vs diplomka
- + future work, open questions
  - learning own embeddings
  - additional methods
    - entity linking from the paper
    - query rewriting and expansion
  - ontology mappings
  - rag with llm
