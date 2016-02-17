---
layout: project_post
title: "Artdealer"
description: "Blacklight Project (solr and rails) implementation for an artdealer's poster collection"
category: project
tags: [solr, blacklight, posters, scraping]
image: /assets/images/projects/artdealer/artdealer.png
---
{% include JB/setup %}


Artdealer is a bit of a tinker-project using [Blacklight](http://projectblacklight.org/) UI to browse posters for sale by an artdealer. This is a personal project to get more familiar with how Blacklight works. While geared to be a discovery layer for MAchine Readable Cataloging (MARC) standardized data, it is easily converted to be a browser for anything that can be indexed by [Apache Solr](https://lucene.apache.org/solr/‎). I applied it to be a cleaner display for an Artdealer's collection (found [here](http://igalcalderpicassowarhol.com/)), which was [scraped](https://github.com/dogrdon/igal-m-atelier/blob/master/scraper.py) and indexed with Solr. 


[See the github repository](https://github.com/dogrdon/artdealer)
