---
layout: post
title: "Introduction to Internet Marketing Content Studies Pt. 1: The Web is (still) not an API"
description: "Suggested content on the web, often ignored or blocked, is both ubiquitous and invisible. Information can take on a different value when aggregated and presented outside of its original context. This post details how I originally sought to take on the collection, analysis, and showcasing those clickbait, suggested content articles that accompany most commercial, high traffic web sites. What I found out is how fragile, bloated, and unpredictable the web is and how it is not anything close to an API if you seek to handle its content like structured data."
category: web
tags: [native ad networks, suggested content, spam, data analysis, web archiving]
---

<figure>
<img class="blog-post" src="" alt=""/><figcaption></figcaption></figure>

### What is it?

Suggestions from native ad networks like Taboola, Outbrain, Revcontent, Content.Ad, Adblade, AdsWift, SiteBooster, ContentBling (I've made up a couple) supply users of popular news sites with articles or 'content' on other web domains. Whether that content is valuable, authentic, "true", or worth consuming is unclear. Whether the domains (examples) they point to are legitimate, reliable, or 'real' is also unclear. 

Native ad content (also called "From around the web", "Suggested content", or "Sponsored content" is generally found bundled up in rows of two or three somewhere around the end of the article right near the comments section. These exist by the virtue of providing their clients (the content providers which deploy them) a source of ad revenue. The content is engineered to maximize numbers of clicks.

Depending on the client, it might point towards other related content within that client's website or network. More often it seems to point towards content that is absurd, false, or otherwise meant almost exclusively to render clicks without regard for the quality, value, or existential merit of the target content.

[Examples]

Most notable are the images used for this content. They migth be titilating, bizarre, nightmarish, or otherwise completely unrelated to their titles.

[Examples]

The headlines are also pretty good:

[Examples]

### Why it's interesting

It's interesting because it's everywhere. It's interesting because it's engineered to be interesting. It's interesting because it's so extremely lowbrow, trashy, and it's baffling that anyone would click on these links at all. Why would this type of garbage be so ubiquitous if it didn't work? Proof that people actually do click on this content is evident in the simple fact that these content seem to be proliferating rapidly and anywhere that a content provider can't seem to advertise or build a subscription base otherwise. 

It is also potentially has a role to play in the recent phenomena of "fake news", which has had consequences far outside of its expectation simply to serve as a spot light for sponsored content on the web.  

Because I found it interesting and because it is not a trivial matter (anymore), I wanted to collect it. But I certainly did not want to waste my time browsing the internet manually to gather these bits of content. So I needed to have a process that would browse the internet for me and collect these absurd nuggest of information. 

### What did I do?

1. Scraped selected websites with know "suggested content" on them for __ days, the more absurd, the better. But I also wanted a sampling of sites that had different political leanings (the list can be found here - you can determine the implicit political leanings yourself). 
2. On any given capture made sure to avoid duplicates (defined by: ____), but left duplicates across harvestings as there might be good information about frequency of a certain link. Of course they could also be more widely deduped later.
3. Wanted to make the resource available to others (for research?) e.g., what content comes up at what times (correlation with news stories?)

### Why?

It is possible that we could learn something about about how these services work by laying out a large number of their products in a searchable database and analyzing them for patterns. I also wanted to explore the connection between types of websites and the types of ads that were served up (e.g., which sites had more quasi-true ads as opposed to others). Finally, I wanted the longitudinal view. That is, to see which ads came and went, for how long, and in what intensities. Also could the same headline be applied to a number of different images or vice versa the same image applied to many different headlines?

That analysis is forthcoming...stay tune for part 2.

### Some main challenges:

The web is still not a great API, particularly for this use case. Because the scraper relies on pulling top n articles and then scraping the third party content from a sampling of those, it will stop working for sites where the layout has changed. Or they might drop an ad content provider. All of these things might be tested for and logged properly. But to some extent, it's not worth that much effort for an experiment like this.

Sometimes they change their marketing strategy and the site begins to show the user overlays (subscribe to get this content, additional ads that users have to click off of to get to site content, etc.)

In many ways PhantomJS is great, but it has issues. Namely that it might fail or suceed inconsistenly. I found that even though I had it running quite well and reliably on my laptop (with OSX), it was much less reliable when run on an Ubuntu server running the exact same version of everything in the script. 

It had a much less greater rate of success scraping native ad content from the article pages on th Ubuntu setup than on the mac setup (hovering around dropping 50% of pages on the former most likely on account of the third party javascript not loading up properly before attempting to scrape -- no matter how long it was set to wait before scraping). It is not clear why this was the case, and I think after a bit of troubleshooting, I just get the sense that PhantomJS is trying to do some complicated stuff, and can't be relied on to give a consistent headless browser experience across the board. 

For the purposes of this experiment, the workaround just forced the scraper to grab more than it probably would be able to properly ingest, in the hopes that it's yield scrape for scrape would be sufficient for a longitudinal analysis even though it errored out on half of the attempts it made every pass.


### Where to next?

- Understand content on a site per site basis or across sites?
- Image analysis, are these images in possession of some clickbaitability?
- Plumbing the evil depths (what happens when you get robots to click on the clicks)
- capture cookie information as part of the SIP
- would want to analyze how these services differ between each other and how they themselves change over time
- ontology of suggested content
- how it makes web pages bloated (way to visualize)
- An exhibit resource (gallery) drawing connections btw items. Ways to grab subjects or topic modeling for things (food, celebrities, health, crime, sex, sex)
- A microcosm of the internet itself, the extreme end if "content". This is the distilled result of these companies best guess of what will draw attention.
- "As a discourse, it's watching machines and reptilian minded marketing initiatives talking to sometime the interests of a specific user (cookies) or perhaps the basest desires of a composite sketch of your average web user."
- probably have a little bit of analysis on what is already there (PT.2)

So stay tuned for part 2, coming this summer. In the meantime, you can preview the analysis here: ____. And the data, refreshed nightly, may be accessed here.


### Notes
<section id="notes"/>
<b>[1]</b> [<a href="#back_1">back</a>]

<b>[2]</b> [<a href="#back_2">back</a>]



#### Internet Marketing Content Studies Bibliography

- https://en.wikipedia.org/wiki/Native_advertising
- http://www.wired.co.uk/article/fake-news-outbrain-taboola-hillary-clinton
- https://digiday.com/media/underbelly-internet-fake-news-gets-funded/
- https://theoutline.com/post/1165/the-web-looks-like-shit
- http://www.lifehack.org/383643/why-use-content-recommendation-networks
- http://programmaticadvertising.org/2015/11/24/if-you-give-a-bot-a-cookie/
- http://motherboard.vice.com/read/the-100-million-content-farm-thats-killing-the-internet
- http://www.adpushup.com/blog/6-best-native-ad-networks-for-online-publishers/
- http://www.safetricks.com/revcontent-native-ads-network-review/ [promotion in disguise]
- http://pointblankseo.com/the-truth-about-content-farms [content-farms not same]
- https://forums.digitalpoint.com/threads/ad-networks-like-taboola-outbrain-who-dont-require-crazy-pageview-min-for-publishers.2668587/
- http://digiday.com/publishers/content-recommendation-ad-holdouts/
- https://www.theatlantic.com/entertainment/archive/2014/11/clickbait-what-is/382545/

