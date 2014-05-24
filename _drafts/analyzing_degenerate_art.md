---
layout: post
title: "The Datenbank Entartete Kunst (Degenarate Art Database)"
description: "The Nazi's attempt to control and or destroy the art they found to be degenerate resulted in a meticulous record keeping of that artwork. The Freie Universität Berlin has undertaken the process of turning that Nazi bookkeeping into a publically accessible database. I took a pass at collecting that data into a sqlite database and went over some of the readily available summary statistics. There are extreme gaps in this data due to incompleteness of the online database itself as well as a lack of information for its artists currently available on services like dbpedia. As such I don't believe it is totally fit for deep analysis. But I think a surface report of some of its attributes is worth the while and provides a proof of concept for datasets in art history. The statistical accumulation of artistic works within a particular context could offer a interesting launch pad for researchers inquiring into that domain."
category: museums
tags: [art, database, museums, data analysis, Neue Galerie, art history, python, linked data]
---
{% include JB/setup %}

<div class="figure">
<img class="blog-post" src="/assets/images/posts/2014/05/degenerate_art_may_2014.png" alt="author's picture of banner at the Neue Galerie Exhibition of Degenerate Art, New York City, 2014. Banner is picture of original degenerate art exhibit in 1937."/>
<div class="figcaption"> Large image of photograph from original Entartete Kunst Exhibition in 1937 displayed at the entrance to the Degenerate Art Exhibit at the Neue Galerie, May 2014.</div></div>


A little while ago I came across [this](http://www.vam.ac.uk/content/articles/e/entartete-kunst/) announcement that the Victoria and Albert Museum had made a digital, browse-able copy of the book the Nazis kept in their program to round up and annihilate European works of art they considered to be 'degenerate'. I hate to give any credit to the Nazis, but in their bookkeeping, they were meticulous. 

My immediate thought was: Would it be possible to get this information into a database for further analysis of what's there? Without access to some pretty heavy duty OCR or a lot of money to throw at something like Amazon Mechanical Turk, the answer was most likely no, for now.

I was pleased to find, however, that the Freie Universität Berlin had undertaken a project to compile the information in these pages into an [online, searchable database](http://www.geschkult.fu-berlin.de/en/e/db_entart_kunst/datenbank/index.html "link to the degenerate art database at the Freie Universität Berlin"), complete with full metadata (where available) for each work of art, as well as the status and current location of the work of art (were it not destroyed or gone missing). It is not a complete database and as of May 2014 has only ~10,300 records of a total ~16,000 works of art in the original bookkeeping.

The related scripts and data can be found [here](http://github.com/droquo/entartete_scraper "link to repository containing scraper and data files for the degenerate art database") in a fairly unkempt repository.

Notes about the data processing:
  - Scraping the database
  To save myself the headache of dealing with installing mechanize and lxml again, I opted to use scraperwiki, so the script is not 100% plug and play.
  
  In scraping the database, I only took some of the primary metadata for the work, that which appears in tabular format. There is added, somewhat variable data below about the provenance of particular artworks, biographical details about the artist etc. Because these were presented in fairly non-sturctured formats, I felt it was not really beneficial to grab this information myself.
  
  -Adding Information to the artists table
  As I was originally interested in taking artwork data and combining it with biographical data about the artists who made the work, I attempted to enrich the artist data with [dbpedia](http://dbpedia.org "link to dbpedia"). Noting that generally the dbpedia resource for an individual follows the pattern of `http://dbpedia.org/resource/Firstname_Surname`. So artist Paul Klee is located at `http://dbpedia.org/resource/Paul_Klee`. As such, I created a pretty naive dbpedia url generator that just used the artist name from the orginal database, switched the firstname and last name and added underscores for spaces. What I came to find was that many of these artists did not have resource pages. And of the ones that did, it was possible that it was not identifying the correct person. For instance the case of http://dbpedia.org/page/Robert_Michel_(K%C3%BCnstler), (vs. http://dbpedia.org/page/Robert_Michel, an American politician). Even then it is such that there is a wikipedia resource for this artist, but not dbpedia resource.
  
  -Geocoding that didn't go so well
  
  
Some take aways

*This post only goes so deep in its analysis. This is a pretty massive topic and really getting at the core of it would require a deep understanding of this point in history, this point in art history, much more information of the biographies of these artists and other such details that are not at my disposal as a hobbyist of degenerate art databases.

*Also, I apologize if collecting this data was somehow problematic. I do not claim to own it and do not have intent to use this data for commercial gain. It is my hope that wrangling this data for this blog post is, if anything, a good promotion for the database itself and welcome any inquiries, notes of admonishment or cease and desist to the e-mail below.

* Some preliminary numbers on the artworks:

Locations, Status, Some details of the Artists

* A deeper dive (scraping wikipedia for relationships):

This really didn't work out, many of these artists are not fully represented on Wikipedia. Some details of the movements, nationalities and birth and deaths of these artists.

Map:

<iframe width='100%' height='600' frameborder='0' src='//droquo.cartodb.com/viz/e8e4e4a8-e228-11e3-ae87-0e73339ffa50/embed_map?title=true&description=true&search=false&shareable=true&cartodb_logo=true&layer_selector=false&legends=true&scrollwheel=true&fullscreen=true&sublayer_options=1&sql=&zoom=2&center_lat=22.59372606392931&center_lon=368.43749999999994' allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

* Discussion:

One of the problems is it's reasonable to hypothesize that many of these artists careers were cut short by this suppression by the Nazis (though it's arguable that some artists were brought more attention by this and it stands to be explored what makes an artist stand out from their milieu).

Some questions for further research:
* Why was printmaking the most predominant art form in the database? (possibly because could be done in quicker succession)
* Age of artists at the time of this program (1937 - dob).

* Conclusion / * Notes:

The use of databases in the research of art history.
Problems with making this data:
*unicode, obviously
*NER was done extremely naively, hence a good number of names probably resolved to someone more famous who reserved the canonical spot for the dbpedia resource (ex. the Robert Michel we were looking for would have been at Robert_Michel_(Künstler) and not http://dbpedai.org/page/Robert_Michel - an American politician. A mistake dbpedia spotlight NER would have also made.)


Find the dataset here
Biggest problem working with this dataset: incompleteness, character encoding (ensure unicode where possible)

Report test:

	most frequent materials or techniques =====
	Lithographie | 2300
	Holzschnitt | 2250
	Radierung | 1462
	Öl auf Leinwand | 925
	Aquarell | 628
	NA | 497
	Farblithographie | 284
	Tusche | 180
	Farbholzschnitt | 122
	Offsetdruck | 100
	Kohle | 99
	Aquarell und Tusche | 93
	Lithographie, koloriert | 82
	Kreide | 74
	Bleistift | 72
