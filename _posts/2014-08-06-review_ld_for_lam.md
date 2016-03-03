---
layout: post
title: "Review: Linked Data for Libraries, Archives and Museums"
description: "A review of the book 'Linked Data for Libraries, Archives and Musuems: How to Clean, Link and Publish Your Metadata' by Seth van Hooland and Ruben Verborgh"
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

### I.
There are a lot of great resources that document linked data fundamentals and best practices out there ([here](http://lodlam.net), [here](http://kcoyle.net/presentations/links.html), [here](http://www.w3.org/standards/semanticweb/), and [here](http://www.clir.org/pubs/reports/pub152/LinkedDataWorkshop.pdf) to name a few).  

But despite all of these resources being widely available and freely accessible online, the discussion still suffers from being a little too abstract or scattered for the beginner or even folks who have regular interaction with data and work within a cultural heritage setting but have not had much experience with linked data. Where linked data is often a practice driven by the particularies of a use case, many resources use examples that are tied too closely to the context in which they are used. Or, on the other hand, to avoid specifying any particular use case, many instructional resources on linked data can stray more towards a self-referencing parade of acronyms, which is great as a refresher, but not for those starting out.

Though I work in a library setting and have sat down with linked data concepts and examples more than a few times already, I don't yet use them in my regular work. Possibly as a result of that, I admitedly have struggled with what linked data exactly is and how to implement it in the work I do. I also definitely could have used a better understanding of its theory and practice in working up my last [post](/museums/2014/05/29/analyzing_degenerate_art/).

The challenge for <i>Linked Data for Libraries, Archives and Museums</i> is to create a coherent introduction and efficient, accessible demonstrations for a practice that is not so easy to summarize in one shot. Linked data is not a single piece of software or one well-established metadata schema. It is rather a mingling of schemas and data structures, varied technologies, and data management practices. It is a workflow where best practices are emerging, but some are still better than others. To make things more difficult, it is a practice for which explanations and principles vary slightly depending on whom you ask (e.g. Librarian or Computer Scientist. Digital Humanist or Web Developer). 

### II.
<i>Linked Data for Libraries, Archives and Museums</i> precipitates many of the challenges a newcomer to linked data might experience. And does so in a way that is driven by pragmatics, using a variety of different example datasets and use cases from different institutions. In this manner, it is nicely assembled for cultural heritage professionals grappling with how linked data might work at their own organizations. By establishing a single, coherent voice and a specific focus on LAM organizations, this book meets a need for providing a basic introduction to a set of ideas where it is often difficult to figure out where one ought to start.

The book layout moves progressively from gathering data and cleaning messy data to reconciling data with canonical taxonomies and ontologies, enriching incomplete data with techniques like Named-entity recognition and finally publishing linked data for others to access and link to. The book takes care to explore the history and existing practices with each practical step and new concept and caps off each chapter with a working case study where a dataset is given treatment using tools and ideas from that chapter. In the case studies you will find the authors' previous work with SPARQL endpoints, [OpenRefine](http://openrfine.org) and related tools from their project, [freeyourmetadata.org](http://freeyourmetadata.org).

Another strength of this book is that it evaluates and makes suggestions on which tools and data formats to use when taking on particular tasks. Though while it makes technology recommendations, it also raises a caveat against allowing technology to guide the way towards linked data. Finally it is pretty good about noting where certain tools fall short, are ceding to newer approaches, or still have a ways to go.

### III.
As a warning, the book spends a fair amount of time using SPARQL endpoints to illustrate how to work with linked datasets. Though in the final chapter on publishing linked data, it sidesteps setting up a SPARQL endpoint and opts for a [JSON backed REST application fed through Node.js](https://github.com/RubenVerborgh/DataPublicationPlatform) as an example for publishing linked data on the web. 

And in discussing publishing data and the use of APIs, the book takes a few swipes at collection aggregators like the [Digital Public Library of America](http://dp.la) and [Europeana](http://www.europeana.eu/) for creating APIs as separate services from the presentation of the data on their main websites. Although I can appreciate the point they are making: that a true REST application should present the data as part and parcel with the display of the objects. And it's also important to note that in simplifying and generalizing this type of system, that it has greater longevity when web technologies evolve. On the other hand, it is possible that a separate API has more advantage when doing aggregate analysis, culling statistics, and generally creating access points that give a wider overview of collection sets than would the REST demo presented in the book. Though I may be unfairly comparing the two. 

However, to the book's credit, presenting a manner for publishing linked data in a way that embraces current web technologies such as JSON and Node.js is a net good in that it shakes the discussion a bit from the tradition of tying linked data so closely to SPARQL and RDF.

### IV.
In the end, this book chooses a natural flow for starting to understand how linked data applies to the work of cultural institutions and the many ways their work and collections fit on the Internet. It goes beyond technical details to provide a broader historical context for linked data and its uses in libraries, archives, and museums. In doing so, it may skim some of the technical details, but as a primer for understanding the wider-picture of how all these peices sit together, it is a great resource. This book would be very suitable as a core text and jump off point in a class on linked data. Or, for that matter, as an open data course with linked data as a focal point, as I do feel it is generalized enough to be somewhat useful for those interested in enriching and linking data sets outside of a LAM setting. Finally, it is of course a good resource for working professionals who want a manageble starting point for figuring out what linked data is and how they can start incorporating it into their workflows and day-to-day efforts. 


<b>Disclosure:</b> <i>I was provided a copy of this book for review purposes. I am otherwise in no way affiliated with the publishers, authors, or any of their related ventures.</i>
