---
layout: post
title: "The Datenbank Entartete Kunst (Degenerate Art Database)"
description: "The Nazi's attempt to control and or destroy the art they found to be degenerate resulted in a meticulous record keeping of that artwork. The Freie Universität Berlin has undertaken the process of turning these records into a publicly accessible database. I took a pass at collecting that data into a sqlite database and went over some of the readily available summary statistics. There are extreme gaps in this data due to some incompleteness of the online database itself as well as a lack of information for its artists currently available on services like DBpedia. As such I don't believe it is totally fit for deep analysis. But I think a surface report of some of its attributes is worth the while and provides a proof of concept for datasets in art history. The statistical accumulation of artistic works within a particular context could offer a interesting launch pad for researchers inquiring into that domain."
category: museums
tags: [art, database, museums, data analysis, Neue Galerie, art history, python, linked data]
---
{% include JB/setup %}

<div class="figure">
<img class="blog-post" src="/assets/images/posts/2014/05/degenerate_art_may_2014.png" alt="author's picture of banner at the Neue Galerie Exhibition of Degenerate Art, New York City, 2014. Banner is picture of original degenerate art exhibit in 1937."/>
<div class="figcaption"> Large image of photograph from original Entartete Kunst Exhibition in 1937 displayed at the entrance to the Degenerate Art Exhibit at the Neue Galerie, May 2014.</div></div>

#### Introduction

In 1937, the Nazis began the public exhibition of works of art which they had seized for being deemed degenerate. It was comprised of the new modern art of the time and was part of a campaign to deride and sanction artists who produced works that were "un-German, Jewish Bolshevist in nature". [1]

This is not a post, however, about the history or the art, as such. Rather it's a brief discussion of the data generated around this art. For those interested in seeing some of these works in person, there is an exhibition of some of the works of art that survived from this period at the [Neue Galerie](http://www.neuegalerie.org/) in New York through September 1, 2014.

#### The Data

A short while ago I came across [this](http://www.vam.ac.uk/content/articles/e/entartete-kunst/) announcement that the Victoria and Albert Museum had made a digital, browse-able copy of the book the Nazis kept in the process of "collecting" these works of art. The meticulous record keeping appeared to make it possible to perform some analytics in the service of Art History research, to serve as a baseline for research into this period of modern art.

At first I considered whether it would it be possible to get this information into a database for further analysis of what's there? Though without access to some pretty heavy-duty OCR or a lot of money to throw at something like [Amazon Mechanical Turk](https://www.mturk.com/mturk/welcome), the answer was most likely no, for now.

I was pleased to find, however, that the Freie Universität Berlin had undertaken a project to compile the information in these pages into an [online, searchable database](http://www.geschkult.fu-berlin.de/en/e/db_entart_kunst/datenbank/index.html "link to the degenerate art database at the Freie Universität Berlin"), complete with full metadata (where available) for each work of art, as well as the status and current location of the work of art (were it not destroyed or gone missing). It is not a complete database and as of May 2014 has only 10,340 records of a total ~16,000 works of art in the original record. Though it is a good chunk of the original and, as such, still quite useful for running some numbers.

Interested to dig in, I scraped off the basic metadata from the online database and put it into a [SQLite database](https://github.com/dogrdon/entartete_scraper/tree/master/data/db "link to sqlite version of degenerate art database, with some additional data"). The related scripts and data can be found [here](http://github.com/dogrdon/entartete_scraper "link to repository containing scraper and data files for the degenerate art database") in a fairly unkempt repository.


#### Notes on Getting and Processing the Data

  - <b>Scraping the database</b> - [scraper here](https://github.com/dogrdon/entartete_scraper/blob/master/scripts/entartete_scraper.py)

  To save myself the headache of dealing with reinstalling [lxml](http://lxml.de/) on a local machine, I opted to use [Scraperwiki](http://scraperwiki.com), so the script is not 100% plug and play.

  In scraping the database, I only took some of the primary metadata for the work; that which is reliably laid out in tabular format. There is additional, somewhat variable data below that ([example here](http://emuseum.campus.fu-berlin.de/eMuseumPlus?service=ExternalInterface&module=collection&objectId=117011&viewType=detailView)) related to the provenance of particular artworks, biographical details about the artist, etc. However, these details were presented in sometimes unstructured formats and sometimes not done in consistent or predictable ways from artist to artist. So I felt it was not really imperative to grab this information, currently.

  - <b>Adding Information to the artists table</b> - [ad hoc enrichment script here](https://github.com/dogrdon/entartete_scraper/blob/master/scripts/artists_extend.py)

  As I was originally interested in taking the artwork data and combining it with biographical data about the artists who made the work, I attempted to enrich the artist data with [DBpedia](http://dbpedia.org "link to DBpedia"). Generally, the DBpedia resource for an individual follows the pattern of `http://dbpedia.org/resource/Firstname_Surname` (so artist Paul Klee is located at `http://dbpedia.org/resource/Paul_Klee`). I created a pretty naive DBpedia url generator using the artist name from the original database, switching the first name and last name and adding underscores for spaces.

  What I came to find was that many of these artists did not have resource pages (out of 663 artists in the database, only 168 appeared to have any kind of DBpedia resource page). Of the ones that did, it was possible that it was not identifying the correct person. For instance, the case of Robert Michel, who would be at `http://dbpedia.org/page/Robert_Michel_(K%C3%BCnstler)`, pointed to a different Robert Michel - `http://dbpedia.org/page/Robert_Michel`, an American politician). In the end, a much more dependable and thorough Named Entity Recognizer (NER) would have to be employed for a more complete set of artist biographical data.

  As a side note, I had first attempted to enrich this data by sticking strictly to the linked data practice of using an RDF graph. While pulling together the graph was very easy with [RDFLib](https://github.com/RDFLib), I found that SPARQL queries skewed towards only returning full records and passed over records that did not have all properties or values for an entity (read: artist). As such, I didn't find it totally practical for this purpose and probably not the main virtue of using a graph database (though I could also be wrong about that.)

  - <b>Geocoding</b> [geocoder here](https://github.com/dogrdon/entartete_scraper/blob/master/scripts/geocoder.py)

  The geocoding approach I used was the Bing API. This was due to the fact that Google has long since placed limits on its geocoding service unless you pay money for it. Out of ~10,000 records, only ~2,000 were geocoded based on whether there was a current location for the artwork (generally the name of a museum). Of the final geocoded results, there were also a few inaccuracies, particularly if the listed location was a private owner and not a well-known museum. At best the geocoded data (as depicted in the map below), is tenuous and not meant for serious research.

  <iframe width='100%' height='600' frameborder='0' src='//droquo.cartodb.com/viz/e8e4e4a8-e228-11e3-ae87-0e73339ffa50/embed_map?title=true&description=true&search=false&shareable=true&cartodb_logo=true&layer_selector=false&legends=true&scrollwheel=true&fullscreen=true&sublayer_options=1&sql=&zoom=2&center_lat=22.59372606392931&center_lon=368.43749999999994' allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

    Translation of Legend
	DRUCKGRAPHIK = PRINTS
	GEMÄLDE = PAINTINGS
	AQUARELL = WATERCOLOR
	ZEICHNUNG = DRAWING
	SKULPTUR/PLASTIK = SCULPTURE / PLASTIC
	TEXTIL = TEXTILE
	MOSAIK = MOSAIC


#### Some Points of Interest in the Data

It's worthwhile to note here that this post only goes so deep in its analysis. This being a fairly massive intersection of Art and World History, really getting at the core of it would require a deeper understanding of this point in time and its context. It would also require a much fuller, more complete dataset. So this is more of a quick and broad treatment, a proof of concept for future work.

Some obvious points of entry now that we have a database we can query are some basic counts of selected columns. Let's start with the overall, current status of works as reported in the database.

	=== Top 10 work statuses ===

| STATUS | COUNT |
|:------|------:|
|Unknown | 5859 |
|destroyed | 1722 |
|Rostock, Museum of Cultural History | 572 |
|Berlin, Prints and Drawings | 335 |
|Private property | 251 |
|Munich , Bavarian State Painting Collections - Pinakothek der Moderne | 147 |
|In the NS - inventory as listed destroyed | 131 |
|Munich , State Graphic Collection | 99 |
|Erfurt, Anger Museum | 60 |
|Weimar, Weimar Classic Foundation | 57 |


The current status of around half of the contents of the current database are `Unknown`. More dismaying, we have a reported 16.7% of the recorded online database having been destroyed.

Next, perhaps we want a count of the art forms employed by the artists.

	=== Top 10 art formats ===

| FORMAT | COUNT |
|:-------|------:|
|Printmaking | 7019 |
|Paintings | 1298 |
|Watercolor | 1034 |
|Drawing | 796 |
|Sculpture / Sculpture | 155 |
|Book | 29 |
|Textile | 5 |
|General | 2 |
|Mosaic | 1 |

I was interested to see that an overwhelming majority of the works here were produced through some form of printmaking (woodcut, lithograph, etching, etc.). There might be a fairly obvious explanation for this. Printmaking, by its nature is far more reproducible of an art form. It is possible to churn out more representations in this format than something like oil painting or watercolor since with a template, you can easily make multiple copies. It is also possible that the works referred to might be reproductions of originals, increasing the representation of this artform in this dataset.

<div class="figure">
<img class="blog-post-sm" src="http://upload.wikimedia.org/wikipedia/en/2/23/%27The_Prophet%27%2C_woodcut_by_Emil_Nolde%2C_1912.jpg" alt="author's picture of banner at the Neue Galerie Exhibition of Degenerate Art, New York City, 2014. Banner is picture of original degenerate art exhibit in 1937."/>
<div class="figcaption"> Emil Nolde The Prophet, woodcut, 1912. via <a href="http://en.wikipedia.org/wiki/Emil_Nolde">Wikipedia</a> EK Inventory No.: <a href="http://emuseum.campus.fu-berlin.de/eMuseumPlus?service=ExternalInterface&module=collection&objectId=121753&viewType=detailView">16302</a></div></div>

On the other hand, it might be the basis for an interesting exploration by someone more familiar with this point in art history. For instance, what were the correlations between modern art and the techniques and technology inherent in printmaking? Was there an increase for any non-trivial reasons? How might application of this technology have facilitated or impacted artistic expression at this time?

Another possibility that might be of interest to explore would be the implications or points of contact with Walter Benjamin's famous essay, <i>The Work of Art in the Age of Mechanical Reproduction</i>. An essay he wrote in 1936, one year before the Nazi exhibition of degenerate art. In it, he concludes that art, where it is more possible to create works through mechanical reproduction (not simply through printmaking, but also through film and photography), is removed from its past as a ritualistic, almost cult-like traditions and becomes more couched in the practice of politics.[2]

Interested in the breakdown of techniques employed by these artists (different from the forms of art), we can also count the materials/techniques category to find frequencies for the various modes of production employed.

	=== Most frequent materials or techniques employed =====

| TECHNIQUE | COUNT |
|:----------|-----:|
|Lithograph | 2300 |
|Woodcut | 2250 |
|Etching | 1462 |
|Oil on canvas | 925 |
|Watercolor | 628 |
|NA | 497 |
|Colour lithograph | 284 |
|Ink | 180 |
|Color woodcut | 122 |
|Offset printing | 100 |
|Coal | 99 |
|Watercolor and ink | 93 |
|Lithograph, colored | 82 |
|Chalk | 74 |
|Pencil | 72 |


With lithography being the most widely used technique, we may be seeing some evidence that many of these works were copies of an artists original. Though here we see that the next most represented techniques are woodcuts and etchings, other forms of printmaking (like the Nolde work above), which may hint at something more interesting in the correlations between modern art, degenerate art, and this artistic technique. Again, a further exploration would probably require a deeper knowledge of this specific domain.

Perhaps we want to see which artists are most widely represented in the database.

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


We are not surprised to see these names here at the top. They are largely the most well-known artists to have been working at this time.[3]

One thing that I find important and fascinating about this exhibition in the present context, however, is that it, unlike other contemporary exhibitions, was not drawn <i>entirely</i> from the most well-known artists of that time (or now, for that matter). Rather, the thread that brings them together is having all been selected for political and sociological reasons at a specific point in history. As such, well-known artists and not so-well-known artists are present in an exhibition as they were within the milieu of that time. In its current manifestation at the Neue Galerie, it is an exhibition somewhat frozen in time (though not without its present day interpretations and narrative). Thus we are able, in some fashion, to evaluate it more like we would our currently working, contemporary artists. With the latter, we don't necessarily have the benefit of history to judge who are the most enduring contributors to a culture (a judgment that's not entirely without it biases and problems, of course). In examining this exhibition as it was, we have a window to explore, perhaps, what it is that makes some artists stand out over others through the course of history.

Speaking simplistically, the counts above may indicate that prolificness is a virtue for enduring in the cultural canon. Though on the other hand, it might be argued that the most prevalent artists in the database are those who were already the most influential at the time, where artists that were more well-known were perceived by the Nazis as posing a greater threat than the more obscure artists at the time.

As another part of this exploration, and one that takes note of the linked data aspect of this data set, we might look at the most common subject terms associated with this set of artists.

	=== Most frequent subject terms ===

| SUBJECT TERM | COUNT |
|:-------|------:|
|German_painters | 58 |
|Modern_painters | 39 |
|German_artists | 21 |
|Expressionism | 20 |
|French_painters | 18 |
|German_sculptors | 18 |
|1887_births | 13 |
|1881_births | 12 |
|German_printmakers | 12 |
|Jewish_painters | 12 |
|German_military_personnel_of_World_War_I | 11 |
|Modern_sculptors | 11 |
|20th - century_painters | 10 |
|Bauhaus | 10 |
|German_Jews | 10 |
|School_of_Paris | 10 |
|Commanders_Crosses_of_the_Order_of_Merit_of_the_Federal_Republic_of_Germany | 9 |
|1889_births | 8 |
|1945_deaths | 8 |

This simple count is interesting in how succinctly it gives us a picture of what art and artists the Nazis targeted. Largely German painters and artists. We also see the artistic movements the Nazis targeted. It is certainly not surprising to see the movements that were most modern and unorthodox in their treatment of the human form and the form of objects like buildings and furniture (Expressionism, Bauhaus). We also see a number of artists born in 1887 and 1881. Were this a more complete dataset, we might take a look more deeply at that dimension.

Interested in seeing which artists were awarded the Commanders Cross (an honor not created until 1951)[4], we can print those names out.

	=== Commanders of the cross subject term ===

|Artist Name|
|:----------|
|Dix, Otto |
|Heckel, Erich |
|Hofer, Karl |
|Marcks , Gerhard |
|Mataré , Ewald |
|Meidner , Ludwig |
|Pechstein, Max |
|Pieper, Josef |
|Sintenis , Renee |

We can also print out the most commonly used titles for artworks to see if there is anything interesting there.

	=== Most frequent artwork titles ===

|TITLE | COUNT |
|:-------|------:|
|Landscape | 65 |
|Self-portrait | 61 |
|Head of a Woman | 33 |
|Still life | 31 |
|Portrait of a Woman | 26 |
|Girls head | 26 |
|Illustration to Curt Hotzel "The City of a good conscience ," Portfolio with 22 lithographs | 22 |
|Bathers | 21 |
|Head | 21 |
|Mother and child | 21 |
|Female Nude | 21 |
|Man's head | 17 |
|Love couple | 16 |
|Postcard | 16 |
|Illustration to " Woe to the world A black and white game in Marmorätzung to a poem by August Stramm . " | 15 |


Here we notice how landscapes, self-portraits and representations of women were common subjects of these artworks. Though it might be that these titles were all of the same work (there are duplicates in the database based on different copies of the same painting, after all). Though in that case, perhaps we can group these by artist to get a better look.

	=== Titles of works grouped by technique and Artist ===

|TECHNIQUE | TITLE | ARTIST | COUNT |
|----------|:-----:|:-------|------:|
|Lithographs | Illustration Curt Hotzel "The City of a good conscience ," Portfolio with 22 lithographs | Hemp , Alfred | 22 |
|NA | Illustration to " Woe to the world A black and white game in Marmorätzung to a poem by August Stramm . " | Meier -Thur , Hugo | 15 |
|Etching | scribe | Nolde, Emil | 15 |
|Lithograph | Walter Hasenclever | Kokoschka, Oskar | 14 |
|Drawing | Postcard | Heckel, Erich | 13 |
|Woodcut | Prophet | Nolde, Emil | 12 |
|Woodcut | Tiger | Marc, Franz | 10 |
|Woodcut | Drinking horse | Marc, Franz | 10 |
|Lithograph | Maria Orska | Kokoschka, Oskar | 10 |
|Lithograph | Max Reinhardt ( breast image ) | Kokoschka, Oskar | 10 |
|NA | Illustration | Masereel , Frans | 10 |
|Etching | sheet from the portfolio " Herbarium " by Grossmann, Expl 13/100 | Grossmann, Rudolf | 10 |
|Etching | Saul and David | Nolde, Emil | 10 |
|Colour lithograph | Two Bathers in Bach | Mueller , Otto | 8 |
|Woodcut | The Bull | Marc, Franz | 8 |
|Woodcut | Hundefängerin | Barlach, Ernst | 8 |
|Woodcut | Candle Dancers | Nolde, Emil | 8 |
|Woodcut | Kindertod | Barlach, Ernst | 8 |
|Lithograph | Christ on the cross | Kokoschka, Oskar | 8 |
|Lithograph | Christ on the Mount of Olives | Kokoschka, Oskar | 8 |
|Lithograph | Two girls half- Nudes | Mueller , Otto | 8 |
|NA | figure study | Lauterbach, Carl | 8 |
|NA | Landscape | Macke, Helmuth | 8 |
|Etching | Solomon and his Women | Nolde, Emil | 8 |
|Etching | ships in the harbor , Flensburg | Nolde, Emil | 8 |

Doing so, we see that some of these were the same work, or a series, from one artist. But some of the more generic titles 'Landscape', we see are the work of more than one artist. The results are not conclusive (or terribly interesting), but we gain a further insight into the general priorities of these artists as well as a more nuanced contrast with these artworks having been deemed degenerate.


#### Some Final Thoughts:

Lacking a firm background in this domain, I am not sure if the ideas expressed above are exceedingly obvious or not. I'd be interested to know if anyone with a background in this might find value in a dataset like this. For anyone who is interested, the database and its schema can be found [here](https://github.com/dogrdon/entartete_scraper/tree/master/data/db "link to sqlite version of degenerate art database, with some additional data"). Again, I do not own this data as it was culled from the Freie Universität Berlin's [online database](http://www.geschkult.fu-berlin.de/en/e/db_entart_kunst/datenbank/index.html "link to the degenerate art database at the Freie Universität Berlin"). The collection of this data and its use here was strictly for educational purposes.



#### References

[1] <a href="http://en.wikipedia.org/wiki/Degenerate_art"> http://en.wikipedia.org/wiki/Degenerate_art </a>

[2] <a href="http://en.wikipedia.org/wiki/The_Work_of_Art_in_the_Age_of_Mechanical_Reproduction">http://en.wikipedia.org/wiki/The_Work_of_Art_in_the_Age_of_Mechanical_Reproduction</a>

[3] <a href="http://cla.calpoly.edu/~mriedlsp/history437/art/Entartete%20Kunst.htm">http://cla.calpoly.edu/~mriedlsp/history437/art/Entartete%20Kunst.htm</a>

[4] <a href="http://en.wikipedia.org/wiki/Order_of_Merit_of_the_Federal_Republic_of_Germany">http://en.wikipedia.org/wiki/Order_of_Merit_of_the_Federal_Republic_of_Germany</a>
