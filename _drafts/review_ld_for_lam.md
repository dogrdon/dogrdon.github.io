---
layout: post
title: "Review: Linked Data for Libraries, Archives, and Museums"
description: "A review of the book 'Linked Data for Libraries, Archives and Musuems: How to Clean, Link and Publish Your Metadata' by Seth van Hooland and Ruben Verbough"
category: linked-data
tags: [linked data, rdf, n-triples, book review, SPARQL, reference]
---
{% include JB/setup %}

<div class="figure float_left"><img class="blog_post" src="/assets/images/posts/2014/08/VanHooland_fullsize_RGB.jpg" title="Image of book cover for Linked Data for Libraries, Archives and Museums" alt="Image of book cover for Linked Data for Libraries, Archives and Museums"/>
<div class="figcaption" style="text-align: left;"><b>Linked Data for Libraries, Archives and Museums</b><br/><br/>
<b>Authors:</b>  <br/>
<b>Paperback:</b> 224 pages <br/>
<b>Publisher:</b> Facet Publishing (June 19, 2014) <br/>
<b>Language:</b> English<br/>
<b>ISBN-10:</b> 1856049647<br/>
<b>ISBN-13:</b> 978-1856049641</div></div>

Though I work in a library setting and have sat down with linked data concepts and examples a few times already, I don't use it outright in my day to day and I admitedly have struggled with what Linked Data exactly is and how to implement some of its practices in the work I do. (I certainly could have used this book in the working of my last post.)

This book is a welcome addition to the literature on the concept of Linked Data <i>particularly</i> in a Library, Archives and Museum's setting, where often the tensions between where LAM organizations need linked data to be and where researchers and computer scientists want linked data to be through the development of the semantic web. Because it is a concept and theory of practice that is intepretted differently depending on whom you ask, it is difficult to learn its components without mixing ideological views. This book at least takes a wide-lens look under a single (although sometimes opinionated) perspective. 

As mentioned above, I've had fleeting interactions with Linked Data in the past, and I have found it a bit unwieldy or often abstract and difficult to translate into real data practices. Coming from an 'Open Data' background, I can appreciate the process of linking datasets and concepts across datasets, but when CSV, JSON and *SQL databases are more of what you are used to, trying to wrap your mind around RDF/XML, SKOS, and SPARQL is more than a little difficult.

One of the stopping points for me was in all of these additional acronyms and the lack of comprehensive documentation around them. Yes, okay, RDF is ____ and it does ____, and SKOS is _____ and it does _____ and SPARQL is a query language for linked datasets. Fine. Fine. Fine. But what I found most difficult is that most explanations of these concepts were self-referencing or not really explained at all <evidence?>.

Linked Data for Libraries, Archives and Museums precipitates these challenges and those a lot of information practitioners might grapple with in trying to see how Linked Data works and what benefit it might have for their organization. 

Not only does it break down linked data practices as an overall process of working with a dataset from soup to nuts (the chapters are outlined in a fashion such that you can start with a non-linked dataset and process it to the point where you can publish it on the web), but it adds a historical context for these metadata schemas and how they relate to other metadata schemas both inside the LAM setting but also outside to more general computer science, data professional concerns.

Framing it within the history of how the web started, it's aspirations to be 'semantic', and the history of classifications systems allowed for a discussion of the current status of Linked Data, what it hopes to accomplish given the past of information management in cultural institutions and where it might fall short or still have a ways to go.

Another strength of this book is that it evaluates and makes suggestions on which tools and formats to use when taking on these particular tasks. For instance, it reviews and evaulauates the results from different Named Entity Recognition services on the web. More helpful is the discussion of publishing Linked Data as some organizations might take a look at what formats and approaches are available and not know which ones have been well-worn, which may need some time, and which represent the future of the practice. 

While I am aware of debates raging over whether XML is in or out, whether one ought to use Turtle instead, and whether JSON and JSON-LD propose a sustainable model for publishing and sharing linked data, it is refreshing to find a resource that at least indicates what might be a better selection over others in considering your approach. It is a piece of the Linked Data information sphere that is either lacking, buried deep in the documentation or just so fragmented that it is not easy to see where the different peices connect most effectively.

Within the jumble of potential approaches, tools, and theories of practice, this book identifies the highlights and gives their history and current relevance to allow the reader to experiment and explore each on their own. In that sense, this book will only take you so far beyond an introduction, but its comprehensiveness, even-handedness, and decisiveness will provide a good baseboard for any linked-data newcomer to pick up where it leaves off in learning more about this way of crafting and sharing cultural heritage objects and their metadata on the web. 

To the books credit, in its final chapters on Publishing linked data and its conclusion, it is opinionated in offerring a framework for viewing the future of Linked Data as it is tied to the future of the Internet, or rather, how linked data can return the world wide web (what we know as the internet today) to its nascent conceits - to being a egalitarian platform for information sharing and linking. I was interested also to see this book take a bit of a swipe at API platforms like that of Europeana and the Digital Public Lirbrary of America, arguing that an architected, multi-API approach is not as future proof as a REST API tied flush to the exact workings of HTTP. That is, a separate URI for resources does not a good API make (no, we're not writing this). Their use, also, of a simple Node.JS application to demonstrate how one might create and API for a collection is another reason why this book, as it ties into the efforts of freeyourmetadata.org and its various Open Refine tools and code bases like this make it a compelling resource for going as shallow or as deep as you'd like.

In the end, this book goes beyond technical details to provide a broader context for Linked Data and its uses in Libraries, Archives, and Museums. In doing so, it does skim some of the technical details, but as a primer for understanding the wider-picture of how all these peices sit together and what peices may soon be giving way to other peices, it is a great resource and one I could certainly picture as a base textbook and jump off point in a class on linked data, or a data and the architecture of the web course that focuses on linked data as a focal point or underlying theme. But this book is also for day-to-day professionals who want a good starting point for figuring out what linked data is and how they can start incorporating it into their workflows in an accessible manner.

**Other presentations, tutorials, and guides on the web are valuable, but for someone getting their feet wet, the domain is a bit scattered and tends to jump right into the deep end. At the end you think you need to create a SPARQL endpoint and then you have no idea why or how.

**While it makes technology recommendations, it also raises the caveat against letting technology guide the way towards linked data. There are many different ways to arrive at linked data and one should do what makes the most sense for your organization (which may preclude setting up your own SPARQL endpoint, for isntance).

**It's possible that this book will be devisive and perhaps step on some toes, but I think it provides enough grounding for its assertions that it's worth a read for the beginner to step through to the intermediate.

**It's final example pulls back enough from the canonic insistence of RDF/SPARQL enough to provide an vision for LD that goes beyond those structures.

Disclosure: I was provided a copy of this book for review purposes. I am otherwise in no way affiliate with the publishers, authors, or any of their related ventures.