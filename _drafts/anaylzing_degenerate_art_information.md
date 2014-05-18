---
layout: post
title: "Light Analysis of the Entartete Kunst Datenbank"
description: "The Nazi's attempt to control and or destroy the art they found to be degenarte resulted in a very meticulous documentation of that artwork. The Freie Universität Berlin has undertaken the process of turning the Nazi bookkeeping into a publically accessible database. I took a pass at collecting that data into a workable form and visualizing it. There are extreme gaps in this data and it is not fit for deep research, but I think a surface report of some of its attributes is worth a short treatment. This is in addition to having visited the Neue Galeries exhibition of some of those recovered works. Concluded that the statistical accumulation of artistic works within a particular context could offer a interesting launch pad for art history researchers, were such databases proliferate."
category: museums
tags: [degenerate art, entartete kunst, data analysis, Neue Galerie]
---
{% include JB/setup %}

*This first came to my attention when I saw [this](http://www.vam.ac.uk/content/articles/e/entartete-kunst/) announcement that the Victoria and Albert Museum had made a digital, browse-able copy of the book the Nazi's kept in their program to annihilate European works of art they considered to be 'degenarate'.

*It got me thinking how interesting it might be to do some quick data analysis to summarize the contents of this well-structured data (I hate to give any credit to the Nazis, but in their bookkeeping, they are meticulous). Without some pretty heavy duty OCR and a ton of money, making these images machine readable was not in the cards for me.

*I was pleased to find, however, that the Freie Universität Berlin had undertaken a project to compile the information in these pages into an [online, searchable database](http://www.geschkult.fu-berlin.de/en/e/db_entart_kunst/datenbank/index.html) complete with full metadata (where available) for each work of art as well as the status and current location (much of it was destroyed, which is discussed below). It is not a complete database and as of April 24, 2014 has only 10,34_ records of a total ____

*Summary of the database
  -EK Inventory corresponds to the Nazi Inventory number, the primary key.

*Notes about data processing:
  -Scraping the database
  -Cleaning the data
  -Adding Information to the artists table
  -Paltry attempt at Geocoding that didn't go so well
  -Visualizing some basic stats

*This post only goes so deep in its visualization. This is a pretty massive topic and really getting at the core of it would require a deep understanding of this point in history, this point in art history, much more information of the biographies of these artists and other such details that are not at my disposal as a hobbyist of degenarate art databases.

*Also, I apologize if collecting this data was somehow problematic. I do not claim to own it and do not have intent to use this data for commercial gain. It is my hope that wrangling this data for this blog post is, if anything, a good promotion for the database itself and welcome any inquiries, notes of admonishment or cease and desist to the e-mail below.

*Some preliminary numbers on the artworks:

Locations, Status, Some details of the Artists

*A deeper dive (scraping wikipedia for relationships):

This really didn't work out, many of these artists are not fully represented on Wikipedia. Some details of the movements, nationalities and birth and deaths of these artists.

*Discussion:

One of the problems is it's reasonable to hypothesize that many of these artists careers were cut short by this suppression by the Nazis (though it's arguable that some artists were brought more attention by this and it stands to be explored what makes an artist stand out from their milieu).

Mistaken identity - the case of http://dbpedia.org/page/Robert_Michel_(K%C3%BCnstler), (vs. http://dbpedia.org/page/Robert_Michel) - having noticed the improbability of the artist being 14 at the time.

(also others with - ages)

Some questions for further research:
*Why was printmaking the most predominant art form in the database? (possibly because could be done in quicker succession)
*Age of artists at the time of this program (1937 - dob).

*Conclusion:

The use of databases in the research of art history.

*Notes
Find the dataset here
Biggest problem working with this dataset: incompleteness, character encoding (ensure unicode where possible)
