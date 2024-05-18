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


-----------------------

Hello,

for a while I have been wrapping my head around how Wikidata prioritizes entities when performing text search on the main Wikidata page (the input box in the right upper corner, e.g. why when writing human the results show human (Q5) on the first line and not something different). I have made a comment few weeks back, and was made familiar that Wikidata uses Elastic Search and probably this is the code mirror repository. I have been looking into it and found profile config files. But I still don't quite understand.

There are profiles for the EntitySearch and EntityPrefixSearch, which to my understand should be the main queries when performing search. Then there are the rescore config files, to my understanding rescore in Elastic is performed on results yilded by the main query. Looking into the files, the rescore functions prioritize entities that have many incoming links and sitelinks (two saturation functions with weights 0.6 and 0.4 while weight of query is 1 and weight of rescore query is 1, the final score should be sum of those scores), but I could not find where the rescore functions are used and whether there are more used somewhere (e.g. appending to a chain of rescore functions). Furthermore, the Elastic bm25 scores are not normalized to [0,1], is there some normalization step before rescoring? Since the rescore with incoming and sitelinks is in the interval [0,1].

Is there someone who would be please willing to explain the process step by step? Martin Gora (talk) 11:28, 13 May 2024 (UTC)

--

@Martin Gora: I don't think the developers are regularly checking this board. Maybe try Wikidata:Report a technical problem? ArthurPSmith (talk) 17:23, 13 May 2024 (UTC)

--

But “I’m curious how this works” is hardly a technical problem IMHO. (Also, given that it’s search-related, Wikidata:Report a technical problem/WDQS and Search would be a slightly better fit than the parent page.)
@Martin Gora: The search team holds monthly “Talk to the Search Platform / Query Service Team” open meetings (usually on the first Wednesday of each month; see [May announcement](https://lists.wikimedia.org/hyperkitty/list/wikitech-l@lists.wikimedia.org/thread/3VB6I5XR2JEQWDMKME4GGPPIH5OJOYH6/)), I think those would be a good venue for your question. Lucas Werkmeister (WMDE) (talk) 09:03, 14 May 2024 (UTC)

--

@Martin Gora CirrusSearch makes use of search profile to tune the retrieval and ranking functions depending on the use-cases. The list of search profiles can be extracted using the [cirrus-profiles-dump API](https://www.wikidata.org/w/api.php?action=cirrus-profiles-dump&verbose=true).
The search profile system has different types (similariry, ft_query_builder, rescore to name a few), knowing how they get assembled is far from trivial but you could get a sense by looking at the contexts section of the API results above, for instance wikibase_fulltext_search is the search context we use to rank results in Special:Search when selecting namespaces holding wikidata entities, if searching for other namespaces we fallback to the default context.
If you are curious you can see extract some debug information from the search system:

see how the query is actually built by appending &cirrusDumpQuery to [your search URL](https://www.wikidata.org/w/index.php?search=bm25&title=Special:Search&profile=default&fulltext=1&cirrusDumpQuery)
see how the explanation of how the scores are computed by appending &cirrusDumpResult&cirrusExplain=pretty to [your search URL](https://www.wikidata.org/w/index.php?search=bm25&title=Special:Search&profile=default&fulltext=1&cirrusDumpResult&cirrusExplain=pretty)
you can also instruct CirrusSearch to a use particular profile by appending the uriParam listed in the overriders from the profiles API, e.g. you can force to use another rescore function by appending &cirrusRescoreProfile=profile_name to [your search URL](https://www.wikidata.org/w/index.php?search=bm25&title=Special:Search&profile=default&fulltext=1&cirrusRescoreProfile=empty)

We generally do not normalize the retrieval scores before applying the rescore window functions indeed, given the wide variety of fields we use, it would be hard, I think, to get to reasonable normalization function. This means that the more words you have in your query the more impactful the text matches will be, which I think is reasonable. For wikis where we have enough data we train a model that results in a decision tree (Q831366) which is less prone to normalization problems.
As suggested by Lucas please feel free to join one of our office hours we would be happy to explain this to you in more details. DCausse (WMF) (talk) 19:39, 14 May 2024 (UTC)

Hello,
I want to thank you - @ArthurPSmith, @Lucas Werkmeister (WMDE), and @DCausse (WMF)) - for your helpful comments. I will definitely try to join the montly meeting.
Best regards, Martin Gora (talk) 11:56, 18 May 2024 (UTC)