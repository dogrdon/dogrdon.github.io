---
layout: post
title: "Getting Back to the Videos..."
description: "Notes, process, and results of trying to determine feasibility and some suggestions for accessing video media through metadata aggregators like the Digital Public Library of America"
category: digital-libraries
tags: [digital preservation, access, archives, dpla, video, audio, digital humanities]
---
{% include JB/setup %}

<div class="figure">
<img class="blog-post" src="" alt=""/><div class="figcaption"></div></div>

###The Premise

Efforts like the Digital Public Library of America (DPLA), it's European counterpart and predecessor Europeana, and other mass digital initiatives to aggregate the collections of many different cultural heritage institutions into one place is providing very new opportunities for discovering and interacting with the contents of these collections. 

With new opportunities for interacting with collections online (such as visualizing collections and collection metadata at a scale and scope previously unthinkable, developing and making obvious new relationships between objects across diverse collections, and allowing the ability for machines to process, calculate, and enhance diverse collections in very new and exciting ways), come the realization that we might not have been preparing for these new possibilities when these possibilities were not realistic enough.

Interesting work has gone into using services (platforms?) like DPLA to explore the geolocation of objects, networks of objects across collections, ability automate and scale out the embedding of contextual information about colleciton topics and subjects across the web, and a great deal of serrendipitous bots for spreading and repurposing collection materials in entertaining ways. Access to relatively lightweight media like images and text provide for a lot of unexpected analyses and reuses of items of these types with relative ease. 

But what I want to focus on is what services like these make available about more size intensive and information complex media like Audio Visual materials, and what deficiencies services like these begin to show us more plainly. Namely that access to these materials, with the sprawl of different publication methods and proprietary software, can be more difficult on the web (where text and images have been a bit more well accounted for) and that institutions in the past have not had the tools or incentives to publish AV materials with similar efficacy.

Though with standards like HTML5, decreasing costs of storage and delivery of large media files over the internet, and new possibilities for machines accessing these media, we have entered a point in time where we should diverege from what has been done before and pursue more standardized methods for publishing and providing access to cultural heritage AV materials online.

###The rationality

This project first started as I'd wanted to explore a way to build a bot that would mash up video and audio files for purposes of novel juxtapositions. Like most bots, this was for creating something silly that had the potential for being something more, given more sophisticated algorithms for pairing audio and video streams and capapcities for learning from interesting combonations. 

But this project quickly wound down given the complexity of attempting direct access to these materials via a web bot. 

###The Problem

- Fairly unresearched comment about how software might be able to help us with the problem of extracting content from AV materials that might not be available through metadata, provenance, and description. 
- Access to the actual video and audio content is restricted, not exactly by copyright and rights (see preliminary data about rights surrounding AV materials in DPLA), but because preceding technology for making these materials available (Flash, Proprietary video and audio playback platforms like JWPlayer, Silverlight, ____, and ____) handle the use case of viewing these items in a browser, but don't allow for very much else and are difficult for web robots to access meaningfully. And what if we want to download them or access them to do something more interesting (which is...)?
- Better metadata or better access to the objects themselves? Well, probably both, but it depends on which questions you are trying to answer (http://it.sla.org/bite/v29n3/metadata/)

####The Approach

First I needed to know how much video and audio are actually on DPLA. Searching via the API gives reasonably limited results (that is, not being greedy is good for others who are accessing the service) and I don't believe it's possible or advisable to wildcard search for everything given a preferred object type.

Next step is to look towards the monthly bulk downloads. This was exactly what I wanted, but this in itself does not lend itself to easy access. Parsing a 200 mb compressed JSON file can take exceptionally long (depending on your hardware, on a 2008 MacBook with only 4gb of RAM, this was pushing at the boundaries of its capacity). Parsing the full 5gb of compressed JSON is going to trounce any normal person's swap. I found this out quickly that loading up these files for exploration in jq was not going to be possible. 

Fortunately, jq's 1.5 release from this past August added streaming capabilities for large JSON files. Instead of parsing and loading the JSON file into RAM for the purposes of querying, you can send it streaming through a set of jq filters to capture the content you are looking for when it crops up in the stream. In a few hours (without crashing your computer) you can write all item and collection titles or rights statements to a text file for text processing, for example.

And there are of course other lightweight tools in python and ruby (yajl=*) that allow you to stream a large JSON file for analyses, data cleaning, and filtering. 

Samples, Samples, Samples. 

jq streaming will allow you to capture values or whole objects of your JSON array as needed. And so this became invaluable for trimming down the DPLA bulk downloads to a more managable size given the slice(s) of information you are looking for. 

From there you can begin to analyze patterns to who is hosting what, and how.

Through this, I found that there were a lot of different ways these collections were hosting their AV materials, some more antagonistic than others to direct, machine access. 

###The Results

- Some sites do provide a download (NARA), where it is applicable and appropriate (some video/audio content, is understandably locked down or behind authentication measures (WGBH, for example)). While it is generally the case that anything available streaming on the internet can be downloaded, some platforms make it much trickier to do in an predictable or automated fashion.
- Others do embed their videos in HTML video tags, making them very easy to access with a scaper (though providing a url directly to the resource in an API would be much better).
- ContentDM accounts for some of these items, but not as many as I had originally thought. 

###Conclusion

-Video and audio files are large, cultural institutions have different purposes for collecting what they do. By this, it makes sense that the storage and distribution of these media is a distributed effort. 

Allowing other services to scrape and store AV materials programmatically also has a lot of potential benefits towards the aim of archiving and preservation (lots of copies keeps stuff safe, that is). 

DH and other research focusing on video and audio could benefit immensely having greater machine access to AV materials.

Ability for machines to browse and dump frames for anaylsis could train and net important solutions for the semi-automated generation of metadata based on access to the content and the computational power to process, analyze, and present important snapshots for human decision making (why do you think captchas make you answer sill questions identifying letters or objects?)

It is imperative that we prepare a new way to work with these media, their rate and volume of creation are going up exponentially and we'll need to rething our relationship with them as a preserved and accessible resource. 
