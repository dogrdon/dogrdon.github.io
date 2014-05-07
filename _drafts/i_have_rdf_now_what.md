---
layout: post
title: "I Have and RDF file. Now What?"
description: "There's a lot of talk about linked data, but one of the common serializations of that, an n-triples rdf file, is still a bit of a black box to me. So I wanted to write a post that explored some very basic operations you can perform to gather some data as RDF and what to do with that data once you have it."
category: linked-data
tags: [linked data, rdf, n-triples]
---
{% include JB/setup %}

Sample Data Example: Gathering extended data for entities from DBPedia. You have a file of names, places, or events and you want to fill our your data with facts about that individual.

Creating the data: Use rdflib and fetch the info from DBPedia with python.

Now you have your RDF file, what does it look like?

What are we going to do with it?

Caveat: I am clear that this may not be the general use case for RDF. To me, it appears that that now that you have your sparkling clean RDF graph, now you connect it to other RDF graphs, and sit happily as your data is now linked. I don't know about any of that. I just want to do a little data analysis.

How do we get data out of the Graph: We query it.

What if I want to create a database for it? There are options for that, but I am not exploring any of them. I really just want to get data out and this is a way to acces wikipedia in a structured way. I am open to alternatives.

Get your data out and append it to a csv file. 
