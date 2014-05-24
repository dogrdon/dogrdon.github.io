---
layout: post
title: "The Datenbank Entartete Kunst (Degenerate Art Database)"
description: "The Nazi's attempt to control and or destroy the art they found to be degenerate resulted in a meticulous record keeping of that artwork. The Freie Universität Berlin has undertaken the process of turning that Nazi bookkeeping into a publically accessible database. I took a pass at collecting that data into a sqlite database and went over some of the readily available summary statistics. There are extreme gaps in this data due to incompleteness of the online database itself as well as a lack of information for its artists currently available on services like dbpedia. As such I don't believe it is totally fit for deep analysis. But I think a surface report of some of its attributes is worth the while and provides a proof of concept for datasets in art history. The statistical accumulation of artistic works within a particular context could offer a interesting launch pad for researchers inquiring into that domain."
category: museums
tags: [art, database, museums, data analysis, Neue Galerie, art history, python, linked data]
---
{% include JB/setup %}

<div class="figure">
<img class="blog-post" src="/assets/images/posts/2014/05/degenerate_art_may_2014.png" alt="author's picture of banner at the Neue Galerie Exhibition of Degenerate Art, New York City, 2014. Banner is picture of original degenerate art exhibit in 1937."/>
<div class="figcaption"> Large image of photograph from original Entartete Kunst Exhibition in 1937 displayed at the entrance to the Degenerate Art Exhibit at the Neue Galerie, May 2014.</div></div>

####Introduction

A short while ago I came across [this](http://www.vam.ac.uk/content/articles/e/entartete-kunst/) announcement that the Victoria and Albert Museum had made a digital, browse-able copy of the book the Nazis kept in their program to round up and annihilate European works of art they considered to be 'degenerate'. I hate to give any credit to the Nazis, but in their bookkeeping, they were meticulous. 

My immediate thought was: Would it be possible to get this information into a database for further analysis of what's there? Without access to some pretty heavy duty OCR or a lot of money to throw at something like Amazon Mechanical Turk, the answer was most likely no, for now.

I was pleased to find, however, that the Freie Universität Berlin had undertaken a project to compile the information in these pages into an [online, searchable database](http://www.geschkult.fu-berlin.de/en/e/db_entart_kunst/datenbank/index.html "link to the degenerate art database at the Freie Universität Berlin"), complete with full metadata (where available) for each work of art, as well as the status and current location of the work of art (were it not destroyed or gone missing). It is not a complete database and as of May 2014 has only ~10,300 records of a total ~16,000 works of art in the original record.

The related scripts and data can be found [here](http://github.com/droquo/entartete_scraper "link to repository containing scraper and data files for the degenerate art database") in a fairly unkempt repository.

####Getting and Processing the Data
  
  - Scraping the database - [scraper here](https://github.com/droquo/entartete_scraper/blob/master/scripts/entartete_scraper.py)
  To save myself the headache of dealing with installing mechanize and lxml again, I opted to use [Scraperwiki](http://scraperwiki.com), so the script is not 100% plug and play.
  
  In scraping the database, I only took some of the primary metadata for the work, that which appears in tabular format. There is added, somewhat variable data below about the provenance of particular artworks, biographical details about the artist etc. Because these were presented in fairly non-sturctured formats, I felt it was not really beneficial to grab this information myself.
  
  - Adding Information to the artists table - [ad hoc enrichment script here](https://github.com/droquo/entartete_scraper/blob/master/scripts/artists_extend.py)
  As I was originally interested in taking artwork data and combining it with biographical data about the artists who made the work, I attempted to enrich the artist data with [dbpedia](http://dbpedia.org "link to dbpedia"). Noting that generally the dbpedia resource for an individual follows the pattern of `http://dbpedia.org/resource/Firstname_Surname`. So artist Paul Klee is located at `http://dbpedia.org/resource/Paul_Klee`. As such, I created a pretty naive dbpedia url generator that just used the artist name from the orginal database, switched the firstname and last name and added underscores for spaces. What I came to find was that many of these artists did not have resource pages. And of the ones that did, it was possible that it was not identifying the correct person. For instance the case of http://dbpedia.org/page/Robert_Michel_(K%C3%BCnstler), (vs. http://dbpedia.org/page/Robert_Michel, an American politician). Even then it is such that there is a wikipedia resource for this artist, but not dbpedia resource.
  
  It is also interesting to note that I had first attempted to enrich this data by sticking strictly to the linked data practice of using an RDF graph, though I found that SPARQL queries skewed towards only returning full records and passed over records that did not have all properties or values we wanted to enrich the database. As such I didn't find it totally practical for this purpose and probably not the main virtue of using a graph database (though I could also be wrong about that.)
  
  - Geocoding [geocoder here](https://github.com/droquo/entartete_scraper/blob/master/scripts/geocoder.py)
  
  The geocoding approach I used was via the Bing API. This, I assume is a mainstay for most off hand geocoding since Google began to place limits on it's geocoding service unless you wanted to start paying some money for it. Out of ~10,000 records, only ~2,000 were geocoded based on whether there was a current location value for the artwork. Of the final geocoded results, there were also a few inaccuracies, particularly if the listed location was a private location. At best the geocoded data (as depicted in the map below), is tenous and not for expert consumption.
  
  Map:

  <iframe width='100%' height='600' frameborder='0' src='//droquo.cartodb.com/viz/e8e4e4a8-e228-11e3-ae87-0e73339ffa50/embed_map?title=true&description=true&search=false&shareable=true&cartodb_logo=true&layer_selector=false&legends=true&scrollwheel=true&fullscreen=true&sublayer_options=1&sql=&zoom=2&center_lat=22.59372606392931&center_lon=368.43749999999994' allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>
  
  
####Some Points of Interest

* This post only goes so deep in its analysis. This being a fairly massive crossroad of Art and World History, really getting at the core of it would require a deeper understanding of this point in time and its context. It would also require a much fuller, more complete dataset. As such, this is more of a quick and broad treatment and a proof of concept on my part.

*Also, I apologize if collecting this data was somehow problematic. I do not claim to own it and do not have intent to use this data for commercial gain. It is my hope that wrangling this data for this blog post is, if anything, a good promotion for the database itself and welcome any inquiries, notes of admonishment or cease and desist to the e-mail below.
	
	Top 10 work statuses =========
	STATUS | COUNT
	Unknown | 5859
	destroyed | 1722
	Rostock, Museum of Cultural History | 572
	Berlin, Prints and Drawings | 335
	Private property | 251
	Munich , Bavarian State Painting Collections - Pinakothek der Moderne | 147
	In the NS - inventory as listed destroyed | 131
	Munich , State Graphic Collection | 99
	Erfurt, Anger Museum | 60
	Weimar, Weimar Classic Foundation | 57
	
	=== Top 10 art formats ===
	FORMAT | COUNT
	Printmaking | 7019
	Paintings | 1298
	Watercolor | 1034
	Drawing | 796
	Sculpture / Sculpture | 155
	Book | 29
	Textile | 5
	General | 2
	B | 1
	Mosaic | 1
	
	=== Most frequent materials or techniques =====
	
	TECHNIQUE | COUNT
	Lithograph | 2300
	Woodcut | 2250
	Etching | 1462
	Oil on canvas | 925
	Watercolor | 628
	NA | 497
	Colour lithograph | 284
	Ink | 180
	Color woodcut | 122
	Offset printing | 100
	Coal | 99
	Watercolor and ink | 93
	Lithograph , colored | 82
	Chalk | 74
	Pencil | 72	
	
=== Artists with most work in the database ===

| ARTIST | COUNT |
|--------|------:|
|Nolde, Emil | 878 |
|Kirchner, Ernst Ludwig | 622 |
|Barlach, Ernst | 590 |
|Heckel, Erich | 587 |
|Kokoschka, Oskar | 509 |
|Mueller , Otto | 312 |
|Pechstein, Max | 268 |
|Schmidt- Rottluff , Karl | 174 |
|Beckmann, Max | 159 |
|Feininger, Lyonel | 138 |
|Grosz , George | 134 |
|Jansen, Franz Maria | 126 |
|Kandinsky, Wassily | 113 |
|Grossmann, Rudolf | 104 |
|Marc, Franz | 99 |
|Dix, Otto | 79 |
|Klee, Paul | 73 |
|Corinth, Lovis | 68 |
|Seewald , Richard | 67 |
|Ehmsen , Heinrich | 66 |
		
	=== Artist with most works under Printmaking ===
	
	ARTIST | COUNT
	Nolde, Emil | 1102
	Heckel, Erich | 796
	Kirchner, Ernst Ludwig | 766
	Barlach, Ernst | 658
	Kokoschka, Oskar | 583
	Mueller , Otto | 414
	Pechstein, Max | 336
	Schmidt- Rottluff , Karl | 250
	Feininger, Lyonel | 235
	Beckmann, Max | 190
	Rohlfs , Christian | 183
	Grosz , George | 180
	Marc, Franz | 145
	Klee, Paul | 137
	Kandinsky, Wassily | 136
	Dix, Otto | 131
	Jansen, Franz Maria | 126
	Grossmann, Rudolf | 114
	Hofer, Karl | 111
	Nauen, Heinrich | 107
	
	=== Most frequent subject terms ===
	
	SUBJECT TERM | COUNT
	German_painters | 58
	Modern_painters | 39
	German_artists | 21
	Expressionism | 20
	French_painters | 18
	German_sculptors | 18
	1887_births | 13
	1881_births | 12
	German_printmakers | 12
	Jewish_painters | 12
	German_military_personnel_of_World_War_I | 11
	Modern_sculptors | 11
	20th - century_painters | 10
	Bauhaus | 10
	German_Jews | 10
	School_of_Paris | 10
	Commanders_Crosses_of_the_Order_of_Merit_of_the_Federal_Republic_of_Germany | 9
	1889_births | 8
	1945_deaths | 8
	
	=== Commanders of the cross subject term ===
	Dix, Otto
	Heckel, Erich
	Hofer, Karl
	Marcks , Gerhard
	Mataré , Ewald
	Meidner , Ludwig
	Pechstein, Max
	Pieper, Josef
	Sintenis , Renee
	
	=== Most frequent artwork titles ===
	TITLE | COUNT
	Landscape | 65
	Self-portrait | 61
	Head of a Woman | 33
	Still life | 31
	Portrait of a Woman | 26
	Girls head | 26
	Illustration to Curt Hotzel "The City of a good conscience ," Portfolio with 22 lithographs | 22
	Bathers | 21
	Head | 21
	Mother and child | 21
	Female Nude | 21
	Man's head | 17
	Love couple | 16
	Postcard | 16
	Illustration to " Woe to the world A black and white game in Marmorätzung to a poem by August Stramm . " | 15
		
	=== Titles by Grouped by technique and Artist ===
	TECHNIQUE | TITLE | ARTIST | COUNT
	Lithographs | Illustration Curt Hotzel "The City of a good conscience ," Portfolio with 22 lithographs | Hemp , Alfred | 22
	NA | Illustration to " Woe to the world A black and white game in Marmorätzung to a poem by August Stramm . " | Meier -Thur , Hugo | 15
	Etching | scribe | Nolde, Emil | 15
	Lithograph | Walter Hasenclever | Kokoschka, Oskar | 14
	Drawing | Postcard | Heckel, Erich | 13
	Woodcut | Prophet | Nolde, Emil | 12
	Woodcut | Tiger | Marc, Franz | 10
	Woodcut | Drinking horse | Marc, Franz | 10
	Lithograph | Maria Orska | Kokoschka, Oskar | 10
	Lithograph | Max Reinhardt ( breast image ) | Kokoschka, Oskar | 10
	NA | Illustration | Masereel , Frans | 10
	Etching | sheet from the portfolio " Herbarium " by Grossmann, Expl 13/100 | Grossmann, Rudolf | 10
	Etching | Saul and David | Nolde, Emil | 10
	Colour lithograph | Two Bathers in Bach | Mueller , Otto | 8
	Woodcut | The Bull | Marc, Franz | 8
	Woodcut | Hundefängerin | Barlach, Ernst | 8
	Woodcut | Candle Dancers | Nolde, Emil | 8
	Woodcut | Kindertod | Barlach, Ernst | 8
	Lithograph | Christ on the cross | Kokoschka, Oskar | 8
	Lithograph | Christ on the Mount of Olives | Kokoschka, Oskar | 8
	Lithograph | Two girls half- Nudes | Mueller , Otto | 8
	NA | figure study | Lauterbach, Carl | 8
	NA | Landscape | Macke, Helmuth | 8
	Etching | Solomon and his Women | Nolde, Emil | 8
	Etching | ships in the harbor , Flensburg | Nolde, Emil | 8



####Some Thoughts:

One of the problems is it's reasonable to hypothesize that many of these artists careers were cut short by this suppression by the Nazis (though it's arguable that some artists were brought more attention by this and it stands to be explored what makes an artist stand out from their milieu).

Some questions for further research:
* Why was printmaking the most predominant art form in the database? (possibly because could be done in quicker succession)
* Age of artists at the time of this program (1937 - dob).


The use of databases in the research of art history.
Problems with making this data:
*unicode, obviously
*NER was done extremely naively, hence a good number of names probably resolved to someone more famous who reserved the canonical spot for the dbpedia resource (ex. the Robert Michel we were looking for would have been at Robert_Michel_(Künstler) and not http://dbpedai.org/page/Robert_Michel - an American politician. A mistake dbpedia spotlight NER would have also made.)

