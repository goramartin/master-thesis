# Necasky meeting 


- intro
  - velice rychle dataspecer, concpetualni modely, muzeme vyuzit to co uz mame - wikidata
  - modelovani je tezke kdyz se dela rucne
  - musime rozlisit konceptualni model ve dvou situacich
    - chci popsat jednu svoji domenu v enterprise domene, nezbyva nez modelovat rucne
    - nebo vytvarit model pro komunikaci pro vymenu dat v prostredi a tam si nemuzu moc vymyslet specifika, nejake spolecne a chceme to prevzit od nekud
      - to spolecne uz je namodelovane
      - i v tom extremu muzu nekde odnekud prevzit
    - cim vic jsme v heterogennim postredi tim vic chceme pouzit to co uz je namodelovano 
  - Prijdou Wikidata
    - neni to jednoduche - nevime co je ontologie a je velka
    - nejak obecne
    - umoznime dataspeceru brat conceptualni model z wikidat
    - analyzujeme co to znamena, naprogramujeme extension a otestujeme
    - rekneme ze navazuje na softwarovy projekt, ktery tohle resil, a delame extension, ale zaroven tato prace bude obsahovat analyzu toho extensionu
      - rozsireni toho co uz mame, ze mame tu ontologii atd.. a le potrebujeme vyhledavat
  - Abychom mohli tvorit potrebujeme vyhledavat
    - nejake problemy atd...
  - pridat popis zadani strucneho
    - chceme vyhledavat tridy
      - dialog
      - metody vyhledavani evaluace
      - evaluace modelovani
      - integrace do dataspeceru
- dataspecer intro
  - uzivalteske hledisko a modelovani vic do hloubky nez v tom intru
    - conceptualni modely - cim, pim, psm
      - jak ten model vlastne vypada
      - abychom vedeli co se tam deje a pak to popsat z pohledu uzivatele
    - co to znamena z pohledu uzivatele, na co to pouzije, atd...
    - obrazky, vystupy
    - popis datove specifikace
    - popis datove struktury
    - popis tvorby datove struktury
  - z analyzovat vnitrni architekturu, ze mame adaptery, editor a dalsi veci, komponenty
  - a ten vstup chceme brat jako wikidata - novy adapter
    - coz znamena 
- information retrieval intro
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


<br>

------------------------

--------------------------

Three options for Wikidata ontology and requirements

----------------------

1. Either introduce the ontology separately - "We have created this ontology" - we just say how the end product looks.
Then we move to the requirements and in the "previous requirements" say, we want to use this ontology in dataspecer.
     - pros: 
       - clear distinctions - ontology x usage in dataspecer
     - cons:
       - the ontology design was influenced by dataspecer and statistics during the process, how to reason about it if we do not know the solution yet

<br>

- **wikidata ontology**
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
      - mozna tohle nechat na pozdeji k designing solutions?
- **requirements and analysis**
  - **puvodni requiremets a existujici reseni s architekturou, jen v rychlosti**
      - koukam na ty requirements a davam k nim veci co uz mame a jejich kratsi analyzu - co vlastne mame uz ted z projektu, proc a pak chci nejakou analysis na to jak vypada ten projekt - architecture
         - funkcni
           - uzivatel to musi umet pouzit v dataspeceru jako ontologii pri tvorbe datove struktury
              - mapovani wikidata ontology na veci z modelu dataspeceru
                - requirements na conceptual model
              - pod requirements na cely process
              - musime mit ontologii
         - kvalitativni
  - **Requirements na vyhledavani a extension**
      - ze uz tam nejake basic vyhledavani je
        - proc nemuzeme pouzit verejna api
      - co se musi rozsirit, a jak aby se nerozbil ten zbytek puvodnich requirements
    - **funkcni pozadavky z hlediska vyhledavani**
      - nasepta mi to koren na zaklade popisu tridy
      - filtrovani na zaklade properties - ze to ma byt AND
      - moznost uprednostnit velmi zname veci
    - **kvalitativni pozadavky z hlediska vyhledavani**
      - musime zvladnou objem ve wikidatech
      - opakovani preprocesingu, predvypocet, zavisi na tom predchozim
      - ma to byt dostatecne rychle


---------------------

2. The entire section will be part of the requirements, and this, there will be requirement - to create ontology from Wikidata, get the ontology, and then second requirement, use this in dataspecer. So the construction will be part of the "previous requirements"
   - pros
      - the text will be more clear
      - we have intermingled

<br>

- **requirements and analysis**
  - **puvodni requiremets a existujici reseni, jen v rychlosti**
      - koukam na ty requirements a davam k nim veci co uz mame a jejich kratsi analyzu - co vlastne mame uz ted z projektu, proc a pak chci nejakou analysis na to jak vypada ten projekt - architecture
         - funkcni
           - uzivatel to musi umet pouzit v dataspeceru jako ontologii pri tvorbe datove struktury
              - pod requirements na cely process
              - musime mit ontologii
                - wikidata ontology intro / analysis (tady hlavne popis z projektu) ??? mozna to dat do te kolonky requirements and analysis, do puvodnich requirements
                  - Dataspecer model
                    - co chceme do dataspeceru aby se to dalo mapovat na strukturu ve wikidatech
                    - coz je neco jako requirement na ten conceptualni model
                    - a zbytek teto sekce je kratsi analyza + vysledek toho co uz mame z projektu
                  - do detailu v jake strukture jsou ty ontologie zakodovane a velikost
                    - nejaky basic model - to co jsem kreslil na schuzce, mozna odkazy, json atd...
                    - pravidla ktera jiy jsou, a ktera jsme pridali
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
                      - mozna tohle nechat na pozdeji k designing solutions?
         - kvalitativni
  - **Requirements na vyhledavani a extension**
      - ze uz tam nejake basic vyhledavani je
        - proc nemuzeme pouzit verejna api
      - co se musi rozsirit, a jak aby se nerozbil ten zbytek
    - **funkcni pozadavky z hlediska vyhledavani**
      - nasepta mi to koren na zaklade popisu tridy
      - filtrovani na zaklade properties - ze to ma byt AND
      - moznost uprednostnit velmi zname veci
    - **kvalitativni pozadavky z hlediska vyhledavani**
      - musime zvladnou objem ve wikidatech
      - opakovani preprocesingu, predvypocet, zavisi na tom predchozim
      - ma to byt dostatecne rychle

--------------------

3. Analysis of the existing project - jen proste rict jak to je a pak rict requirements na to vyhledavani
   - nedelat to jako requirements
   - ale pospat to co uz je
   - architektura 
   - ta ontologie
   - atd... 


- Requirements and analysis
  - Popis jiz existujiciho reseni
      - **wikidata ontology**
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
              - mozna tohle nechat na pozdeji k designing solutions?
    - Jak se ta ontologie mapuje na dataspecer
    - Architecture of integration 
      - popsat existujici servicy
      - a co delaji
      - a proc
- **Requirements na vyhledavani a extension**
     - ze uz tam nejake basic vyhledavani je
       - proc nemuzeme pouzit verejna api
     - co se musi rozsirit, a jak aby se nerozbil ten zbytek
   - **funkcni pozadavky z hlediska vyhledavani**
     - nasepta mi to koren na zaklade popisu tridy
     - filtrovani na zaklade properties - ze to ma byt AND
     - moznost uprednostnit velmi zname veci
   - **kvalitativni pozadavky z hlediska vyhledavani**
     - musime zvladnou objem ve wikidatech
     - opakovani preprocesingu, predvypocet, zavisi na tom predchozim
     - ma to byt dostatecne rychle


<br>

------------------------

------------------------

<br>

- search solutions design
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
- implementation
  - architecture of the services
    - where runs what
  - designing a front end of the search
  - v cem to je napsane
  -  jake databaze?
  - pruvodce pro programatora
    - mame uz dokumentaci na githubu
  - uzivatelska dokumentace?
    - obrazky
- evaluace 
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
- related work
  - vsechno co mam od paperu
  - hlavne ontology search a class importance, entity linking and rag.
  - z pohledu hledani je to obecne vsechno co mame z retrievalu
  - taky nutnost zminit YAGO
- conclusion
  - ze jsme to rozsirili vyzkumny projekt vs diplomka
  - + future work, open questions
    - learning own embeddings
    - additional methods
      - entity linking from the paper
      - query rewriting and expansion
    - ontology mappings
    - rag with llm
