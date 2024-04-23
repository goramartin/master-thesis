# 5. meeting 

This meeting I would like to talk about:
1. Brief overview of what I did.
2. Harmonogram    
3. Wikidata insights
4. Tests
5. Diploma text

## Brief overview of what I did

- From previous meeting:
  - [x] Test language models if they can be used for free

- From my self:
  - [x] Look into Wikidata labels/aliases/descriptions co-ocurrences.
  - [x] Thinkg about diploma table of contents.

## Harmonogram

- Finish the last part of research project
  - end of april
- Programming of diploma
  - end of may
- Text writing
  - 18.7.

## Wikidata insights


### Number of instances

- depics number of instances of a class, where the instances are also classes

```
{"n":1249206,"id":113145171,"name":"type of chemical entity"},
{"n":1026464,"id":7187,"name":"gene"},
{"n":761264,"id":8054,"name":"protein"},
{"n":138395,"id":59199015,"name":"group of stereoisomers"},
{"n":71958,"id":4164871,"name":"position"},
{"n":50142,"id":277338,"name":"pseudogene"},
{"n":45755,"id":427087,"name":"non-coding RNA"},
{"n":28269,"id":2996394,"name":"biological process"},
{"n":22617,"id":417841,"name":"protein family"},
{"n":18252,"id":294414,"name":"public office"},
{"n":16382,"id":112193867,"name":"class of disease"},
{"n":13857,"id":66826848,"name":"protein obsoleted in UniProtKB, SwissProt, TrEMBL"},
{"n":11244,"id":14860489,"name":"molecular function"},
{"n":10748,"id":67015883,"name":"group or class of enzymes"},
```

### Number of same labels

```
{"n":38241,"value":"hypothetical protein, conserved"},
{"n":34885,"value":"hypothetical protein"},
{"n":12027,"value":"conserved plasmodium protein, unknown function"},
{"n":4982,"value":"protein of unknown function"},
{"n":3732,"value":"conserved protein, unknown function"},
{"n":2509,"value":"pir protein"},
{"n":2224,"value":"hypothetical protein, unknown function"},
{"n":1635,"value":"unnamed protein product"},
{"n":1632,"value":"hypothetical protein, conserved in t. vivax"},
{"n":1383,"value":"hypothetical protein, conserved (fragment)"},
{"n":1271,"value":"plasmodium exported protein, unknown function"},
{"n":1197,"value":"hypothetical rna"},
{"n":1123,"value":"trypanosomal vsg domain containing protein, putative"},
{"n":888,"value":"expressed protein"},
```

### Number of same descriptions

```
{"n":1246275,"value":"chemical compound"},
{"n":778140,"value":"__empty__"},
{"n":27628,"value":"protein-coding gene in the species mus musculus"},
{"n":22918,"value":"protein-coding gene in the species rattus norvegicus"},
{"n":20164,"value":"protein-coding gene in the species homo sapiens"},
{"n":18675,"value":"interpro family"},
{"n":16923,"value":"non-coding rna in the species homo sapiens"},
{"n":16051,"value":"pseudogene in the species homo sapiens"},
{"n":15546,"value":"gene of the species macaca nemestrina"},
{"n":14458,"value":"bioactive natural product"},
{"n":12932,"value":"non-coding rna in the species mus musculus"},
{"n":12088,"value":"fungal protein found in aspergillus oryzae rib40"},
{"n":11841,"value":"human disease"},
```

### Number of same aliases

```
{"n":2291795,"alias":"__empty__"},
{"n":177278,"alias":"hypothetical protein"},
{"n":20968,"alias":"predicted protein"},
{"n":7831,"alias":"conserved hypothetical protein"},
{"n":3615,"alias":"unspecified product"},
{"n":3474,"alias":"transcriptional regulator"},
{"n":3273,"alias":"hypothetical transcript"},
{"n":2982,"alias":"abc transporter atp-binding protein"},
{"n":2929,"alias":"expressed protein"},
{"n":2293,"alias":"pir protein"},
```

### Number of same tuples (label, description)
```
{"n":21413,"value":"hypothetical protein __empty__"},
{"n":6605,"value":"hypothetical protein, conserved __empty__"},
{"n":1634,"value":"unnamed protein product __empty__"},
{"n":1197,"value":"hypothetical rna __empty__"},
{"n":1052,"value":"trypanosomal vsg domain containing protein, putative __empty__"},
{"n":889,"value":"variant surface glycoprotein (vsg, pseudogene), putative __empty__"},
{"n":735,"value":"trypanosomal vsg domain/trypanosome variant surface glycoprotein c-terminal domain containing protein, putative __empty__"},
{"n":726,"value":"trypanosome variant surface glycoprotein (a-type), putative __empty__"},
{"n":694,"value":"unspecified product __empty__"},
{"n":671,"value":"retrotransposon hot spot protein, putative __empty__"},
{"n":639,"value":"rif __empty__"},
```

### What to take from this.

- The ontology is dominated by genes/proteins/chemicals
- Maybe we should consider only the general terms?
  - remove the genes and proteins and chemicals
  - and keep only the base classes
- Candidate selection
  - possibly impossible to generate reasonable amount of candidates even for a specific query.


## Tests

- Devise queries
  - or
- Let users test it

```
Concept input bar:
    [ name ], [ short description ]

Properties input bar
    [ name ], [ short description ] (select as typing)
     (add button)
```

## Table of contents diploma

```
- intro
  - velice rychle dataspecer, concpetualni modely, muzeme vyuzit to co uz mame - wikidata
  - neni to jednoduche - nevime co je ontologie a je velka
  - umoznime dataspeceru brat conceptualni model z wikidat
  - analyzujeme co to znamena, naprogramujeme extension a otestujeme
- dataspecer intro
  - uzivalteske hledisko
  - conceptualni modely - cim, pim, psm
  - a ten vstup chceme brat jako wikidata - novy adapter
- information retrieval intro
  - jak jsme videli wikidata jsou velke - chceme cislo, pocet trid bez vetsiho detailu
  - chceme metody IR
  - chceme konkretni metody ktere vyuzijeme
- wikidata analysis
  - do detailu v jake strukture jsou ty ontologie zakodovane a velikost
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
- solutions
  - achitecture
  - solutions in depth and why
- implementation
  - pruvodce pro programatora
    - orientace
    - kam sahnout kdyz chceme neco upravit
- testing
- related work
- conclusion
  - + future work, open questions
```

- Questions:
  1. Where to place related work?
     - i want to mention and reason about some details from the papers when designing solutions
  2. How to combine wikidata intro and wikidata analysis?
  3. Should I talk about the solution from research project?
  4. Depth of the information retrieval intro
     - large field
  5. General depth of formality?
     - formal ontologies, dataspecer, rdf?
     - depth of language models
  6. Can i use chatgpt?
     
- chybi analyza requirements a co je cilem te prace, information retrieval intro, pozadavky na to co chceme
analyza pozadavku
- analyza wikidat z pohledu pozadavku
- wikidata intro spojit s analyzou
- related work az na konci
- veci z previous research projektu
  - skoro vsechno
- depth infromation retrieval
  - jen rict to co potrebuji a odkazovat se referencema
- s pomoci wikidat zkonstruujeme conceptualni model
  - do urcite miry detaily abychom to mohli pouzit v textu
  - ten jejich model
  - a jak vidim ten konceptualni model a jak se to mapuje
  - tohle spada do pozadavku


## To the next meeting

- Promyslet strukturu textu