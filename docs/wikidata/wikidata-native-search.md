# Wikidata native search

This file contains information about the native search in the wikidata.

- Me

Hello everyone,

I wanted to ask if there is a way to find out index configuration/mappings files of the main ElasticSearch in Wikidata. Either, the one when browsing to the main wikidata website (the panel on the upper right corner) or the mediawiki actions api wbsearchentities. I wonder mainly how the labels/aliases/descriptions are stored in the index and what is the returned entities priority/ordering process when searching, e.g. how come when searching a word "human", it returns human (Q5) as the top result. I would appreaciate any response.

Have a nice day, Martin. Martin Gora (talk) 09:27, 12 March 2024 (UTC)

- Answer

The ElasticSearch databases are accessible from PAWS. Here's the Wikidata ElasticSearch mappings: https://paste.toolforge.org/view/37b8a626 .

Configuration I guess are based on ([1](https://github.com/wikimedia/mediawiki-extensions-WikibaseCirrusSearch/tree/master/src/config)) and ([2](https://github.com/wikimedia/mediawiki-extensions-CirrusSearch/tree/master/profiles)). Didnt't look too closely, hopefully someone will point out if it's the wrong place.

Results with lots of sitelinks and incoming links seems to be scored higher. Infrastruktur (talk) 11:56, 12 March 2024 (UTC)