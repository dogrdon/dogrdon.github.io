---
layout: post
title: "Review: Linked Data for Libraries, Archives, and Museums"
description: "A review of the book 'Linked Data for Libraries, Archives and Musuems: How to Clean, Link and Publish Your Metadata' by Seth van Hooland and Ruben Verbough"
category: linked-data
tags: [linked data, rdf, n-triples, review, SPARQL, reference, libraries, museums, archives]
---
{% include JB/setup %}

<div class="figure float_left"><img class="blog_post" src="/assets/images/posts/2014/08/ldlam.jpg" title="Image of book cover for Linked Data for Libraries, Archives and Museums" alt="Image of book cover for Linked Data for Libraries, Archives and Museums"/>
<div class="figcaption" style="text-align: left;"><b>Linked Data for Libraries, Archives and Museums: How to Clean, Link and Publish your Metadata</b><br/><br/>
<b>Authors:</b> Seth van Hooland and Ruben Verborgh <br/>
<b>Paperback:</b> 272 pages <br/>
<b>Publisher:</b> ALA Editions (07/08/2014) <br/>
<b>Language:</b> English<br/>
<b>ISBN-13:</b> 978-0-8389-1251-5 </div></div>

### I (The discussion)
There are a lot of great resources out there that document Linked Data fundamentals and best practices ([here](http://lodlam.net), [here](http://kcoyle.net/presentations/links.html), [here](http://www.w3.org/standards/semanticweb/), and [here](http://www.clir.org/pubs/reports/pub152/LinkedDataWorkshop.pdf) are a good start). As an offshoot of the semantic web, an aspiration for the world wide web and the internet that has been around for a while [1], linked data is not a buzz word or a passing fad. 

But despite all of these resources being widely available and freely accessible online for some time now, I've found that the discussion still suffers from being too unattainable or scattered for the beginner or even folks who have regular interaction with data and or work within a Library, Museum, or Archive setting. 

Though I work in a library setting and have sat down with linked data concepts and examples more than a few times already, I don't use it outright in my day to day work. Possibly as a result of that, I admitedly have struggled with what Linked Data exactly is and how to implement some of its practices in the work I do. (I certainly could have used a better understanding of its theory and practice in working up my last [post](/museums/2014/05/29/analyzing_degenerate_art/).)

This book's challenge is to create a coherent introduction and demonstration of a concept that is difficult to pin down because it is not a single technology but rather a set of different practices and potential technologies for manifesting those practices. Furthermore it is a concept and theory of practice that is interpretted slightly differently depending on whom you ask, (Librarian or Computer Scientist, Digital Humanist, or Web Developer). Thus it it is difficult to learn from various resources across the web without mixing ideological views from resource to resource. This book, instead, takes a wide-lens look under a single (although not without its own opinion and biases) perspective.

### II (The contribution)

Linked Data for Libraries, Archives and Museums precipitates many of the challenges a newcomer to Linked Data might experience. And does so in a way that is driven by pragmatics, a plus for information professionals grappling with how Linked Data might work at their organization. 

The book layout moves progressively from gathering data, cleaning data, reconciling messy data with canonical taxonomies and ontologies, enriching data with techniques like named entity recognition and finally publishing data after going through those steps. The book takes care to explore the history and existing practices within the context of each practical step in working with data and caps each chapter with a working case study where a data set is given treatment using a variety of tools to illustrate the chapter's contents. Therein you'll find the authors' previous works with SPARQL endpoints, OpenRefine and related tools through their website [freeyourmetadata.org](http://freeyourmetadata.org).

Another strength of this book is that it evaluates and makes suggestions on which tools and formats to use when taking on these particular tasks. For instance, it reviews and evaulauates the results from different Named Entity Recognition services on the web. More helpful is the discussion of publishing Linked Data as some organizations might take a look at what formats and approaches are available and not know which ones have been well-worn, which may need some time, and which represent the future of the practice. 

While I am aware of debates raging over whether XML is in or out, whether one ought to use Turtle instead, and whether JSON and JSON-LD propose a sustainable model for publishing and sharing linked data, it is refreshing to find a resource that at least indicates what might be a better selection over others in considering your approach. It is a piece of the Linked Data information sphere that is either lacking, buried deep in the documentation or just so fragmented that it is not easy to see where the different peices connect most effectively.

### III (What worked well)

To the books credit, in its final chapters on Publishing linked data and its conclusion, it is opinionated in offerring a framework for viewing the future of Linked Data as it is tied to the future of the Internet, or rather, how linked data can return the world wide web (what we know as the internet today) to its nascent conceits - to being a egalitarian platform for information sharing and linking. I was interested also to see this book take a bit of a swipe at API platforms like that of Europeana and the Digital Public Lirbrary of America, arguing that an architected, multi-API approach is not as future proof as a REST API tied flush to the exact workings of HTTP. That is, a separate URI for resources does not a good API make (no, we're not writing this). Their use, also, of a simple Node.JS application to demonstrate how one might create and API for a collection is another reason why this book, as it ties into the efforts of freeyourmetadata.org and its various Open Refine tools and code bases like this make it a compelling resource for going as shallow or as deep as you'd like.

### IV (What needed more work)

The book spends a fair amount of time on SPARQL endpoints, though in the final chapter on publishing linked data, it sidesteps something like setting up a SPARQL endpoint instead opting for a [JSON backed REST API fed through Node.js](https://github.com/RubenVerborgh/DataPublicationPlatform) as an example for publishing Linked Data on the web. It is also in this final chapter on publishing that the book takes a few swipes at collection services like the Digital Public Library of America and Europeana for approaching an API as a separate service to their website. While I can appreciate the point they are trying to make: that a true REST API should be part and parcel with the display of the objects, it's also possible that a separate API has more advantages when doing aggregate analysis over collection sets than would the REST API presented in the book. 

However, that this book does present a manner for publishing Linked Data in a manner that embraces more widely used web technologies such as JSON and Node.js is also a potential good as it removes the barriers to entry presented by things like SPARQL and RDF

### V (Conclsion)

In the end, this book goes beyond technical details to provide a broader context for Linked Data and its uses in Libraries, Archives, and Museums. In doing so, it does skim some of the technical details, but as a primer for understanding the wider-picture of how all these peices sit together and what peices may soon be giving way to other peices, it is a great resource and one I could certainly picture as a base textbook and jump off point in a class on linked data, or a data and the architecture of the web course that focuses on linked data as a focal point or underlying theme. But this book is also for day-to-day professionals who want a good starting point for figuring out what linked data is and how they can start incorporating it into their workflows in an accessible manner.

While it makes technology recommendations, it also raises the caveat against letting technology guide the way towards linked data. There are many different ways to arrive at linked data and one should do what makes the most sense for your organization.

Within the jumble of potential approaches, tools, and theories of practice, this book identifies the highlights and gives their history and current relevance to allow the reader to experiment and explore each on their own. In that sense, this book will only take you so far beyond an introduction, but its comprehensiveness, even-handedness, and decisiveness will provide a good baseboard for any linked-data newcomer to pick up where it leaves off in learning more about this way of crafting and sharing cultural heritage objects and their metadata on the web. 

Where looking towards scattered presentations, tutorials, and guides on the web are valuable for those looking to reference certain ideas, or see how some institutions have incorporated Linked Data into their collections. For someone getting their feet wet, the domain is a bit scattered and tends to jump right into the deep end. Many resources tend to be ingredients lists, or recipes that point to ingredients and cooking materials you might not have access to. This book, on the other hand, is in some respects a full cookbook, beginners cookbook, but the kind that introduces you to the history and the culture surrounding the dishes being made and the different methods for preparation.

<b>Disclosure:</b> <i>I was provided a copy of this book for review purposes. I am otherwise in no way affiliated with the publishers, authors, or any of their related ventures.</i>

[1] [http://en.wikipedia.org/wiki/Semantic_Web#History](http://en.wikipedia.org/wiki/Semantic_Web#History)