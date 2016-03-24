---
layout: post
title: "Linked-Data on the web: JSON-LD"
description: "For now a possible series trying to digest the purpose of various serializations, infrastructure/architecture, practice, community, and goals in Linked Data."
category: digital-libraries
tags: [linked-data, access, metadata, interoperability, json-ld, practice]
---

Linked Data is a complicated thing and that's largely because it has so many different applications an purposes. I can't get into all of them here, but the Library context for linked data is only one part of a larger whole.

A lot of the discussion is based on from where implementing Linked Data makes sense. 

Is it a new type of database? A backend only?
Is it a published reference readable by machines and systems?
Is it a way to access web pages and for who or what?
What applications can connect to it and what can they do?
Does it replace a technology or supplement it?
What are the scalability concerns and can they be overcome for the purpose we want to use Linked Data for?

JSON-LD is a partciular type of serialization for Linked Data. But is it really a JSON version of Linked Data, or just a better for of JSON.

And what is linked data? It is born of the Semantic Web and how to connect resources more intelligently. For what purpose?

I have always struggled with Linked Data, and a large part of it isn't really the theory so much as the various implementations. Triplestores and SPARQL being the more irritating of all the parts of this discussion. I could join the pile on ov RDF-XML, but I'll save it partly because I only recently realized that RDFXML is not what linked data are about. 

There is a whole world of folks talking up JSON-LD as a great SEO tool (because schema.org and blargh). But I don't think this does JSON-LD and the project of a Semantic Web justice. 

So this is a discussion of the different components of Linked Data, which ones ought to be prioritized and why JSON-LD is no the evil cousin trying to sell off the family property to the highest bidder.

What is it capable of and what does it lack. And how it might be better used to avoid having to expose your clients to things like SPARQL (AKA: are linked data fragments reallty the solution, or is it about defining the space and the practice).

This could also just be about the interesting components of JSON-LD and what it provides. Folks talk about querying any triple in the world, so long as you have a sparql endpoint. But isn't that what the web is already for? What's the point of strapping a lawnmower engine on top of your cars v6? It seems rather unecessary. Or does it? I don't know.


What linked data doesn't solve are poorly described entities, there's still a lot of human interjection there...even with some hardcore reconciliation.

What can JSON-LD do for you? Other options, what are we trying to accomplish with our LD architecture and is it what users want?


#### JSON-LD Bibliography:

(see pocket for now)

https://github.com/lobid/lodmill
check out bibframe and bibjson
hypermedia-driven web APIs