---
layout: post
title: "Review: Linked Data for Libraries, Archives, and Museums"
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

### I
There are a lot of great resources that document Linked Data fundamentals and best practices out there ([here](http://lodlam.net), [here](http://kcoyle.net/presentations/links.html), [here](http://www.w3.org/standards/semanticweb/), and [here](http://www.clir.org/pubs/reports/pub152/LinkedDataWorkshop.pdf) are a good start).  

But despite all of these resources being widely available and freely accessible online, the discussion still suffers from being a little too out of reach or scattered for the beginner or even folks who have regular interaction with data and or work within a Library, Museum, or Archive setting. Where Linked Data is often a practice driven by the particularies of a use case, many of these resources use examples that are tied too closely to the example in which they being used. On the other hand, to avoid specifying any particular use case, many instructional resources on linked data can stray more towards a self-referencing parade of acronyms.

Though I work in a library setting and have sat down with linked data concepts and examples more than a few times already, I don't use it outright in my day to day work. Possibly as a result of that, I admitedly have struggled with what Linked Data exactly is and how to implement it in the work I do. (I definitely could have used a better understanding of its theory and practice in working up my last [post](/museums/2014/05/29/analyzing_degenerate_art/).)

The challenge for <i>Linked Data for Libraries, Archives and Museums</i> is to create a coherent introduction to and efficient demonstration of a practice that is not so easy to summarize in one shot. Linked Data is not a set piece of software or one well established metadata scheme. It is rather a mingling of metadata concepts and schemas, varied technologies, and data management practices for which best practices are emerging, but some are better than others. To make things more difficult it is a practice in data management that for which interpretations vary slightly depending on whom you ask, (Librarian or Computer Scientist. Digital Humanist, or Web Developer). 

### II
Linked Data for Libraries, Archives and Museums precipitates many of the challenges a newcomer to Linked Data might experience. And does so in a way that is driven by pragmatics that use a variety of different datasets from various institutions, it is a plus for cultural heritage professionals grappling with how Linked Data might work at their organization. By establishing a single coherent voice and a specific focus on LAM organizations, this book meets a need for providing a basic introduction to a set of ideas where it is often difficult to figure out where one ought to start.

The book layout moves progressively from gathering data, cleaning data, reconciling messy data with canonical taxonomies and ontologies, enriching data with techniques like named entity recognition and finally publishing data for others to access and link to. The book takes care to explore the history and existing practices within the context of each practical step in working with data and caps each chapter with a working case study where a data set is given treatment using a variety of tools to illustrate the chapter's contents. Therein you'll find the authors' previous works with SPARQL endpoints, OpenRefine and related tools through their website [freeyourmetadata.org](http://freeyourmetadata.org).

Another strength of this book is that it evaluates and makes suggestions on which tools and data formats to use when taking on these particular tasks. Though while it makes technology recommendations, it also raises the caveat against letting technology guide the way towards linked data. Finally it is pretty good about noting where certain tools fall short or have a ways to go.

### III (What needed more work)

The book spends a fair amount of time on SPARQL endpoints, though in the final chapter on publishing linked data, it sidesteps setting up a SPARQL endpoint and opts for a [JSON backed REST API fed through Node.js](https://github.com/RubenVerborgh/DataPublicationPlatform) as an example for publishing Linked Data on the web. To the books credit, in this example of published linked data and its conclusion, it is opinionated in offerring a framework for viewing the future of Linked Data as it is tied to the future of shared and connected datasets on the Internet. As such, it presents an example of a REST API (?) that ties the presentation of the data to the browser to the same request that a machine would make to obtain the same data in Turtle, RDF-XML or JSON.

Though in discussing publishing data and the use of APIs, the book takes a few swipes at collection linkers like the [Digital Public Library of America](http://dpla.org) and [Europeana]() for approaching an API as a separate service to the presentation of the data in a browser. While I can appreciate the point they are trying to make: that a true REST API should be part and parcel with the display of the objects, and in being simplified and generalized, it has greater longevity. On the other hand, it's possible that a separate API has more advantages when doing aggregate analysis and over collection sets than would the REST demo presented in the book. 

However, that this book does present a manner for publishing Linked Data in a manner that embraces more widely used web technologies such as JSON and Node.js is also a potential good as it removes the barriers to entry presented by things like SPARQL and RDF

### IV
In the end, this book chooses a natural flow for starting to understand how linked data fits into the work of institutions and the many ways it fits on the Internet. It goes beyond technical details to provide a broader historical context for Linked Data and its uses in Libraries, Archives, and Museums. In doing so, it may skim some of the technical details, but as a primer for understanding the wider-picture of how all these peices sit together, it is a great resource and one I could certainly picture as a core text and jump off point in a class on linked data. Or, for that matter, as an open data course with linked data as a focal point, as I do feel this book is generalized enough to be somewhat useful for those interested in enriching and linking data sets outside of a LAM setting. It is also a good resource for working professionals who want a good starting point for figuring out what linked data is and how they can start incorporating it into their workflows and day-to-day work.


<b>Disclosure:</b> <i>I was provided a copy of this book for review purposes. I am otherwise in no way affiliated with the publishers, authors, or any of their related ventures.</i>
