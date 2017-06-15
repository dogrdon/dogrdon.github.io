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

Suggestions from native ad networks like Taboola, Outbrain, Revcontent, Content.Ad, and Adblade supply users of popular news sites with promoted articles or 'content' on other web domains. Whether that content is valuable, authentic, "true", or worth consuming is unclear. Whether the domains (examples) they point to are legitimate, reliable, or 'real' is also unclear. 

Native ad content (also called "promoted links from around the web", "sponsored links", or "sponsored content" is generally found bundled up in rows of two or three somewhere around the end of the article somewhere near the comments section. They provide their clients (the content providers which deploy them on their sites) a source of ad revenue. The content, it seems, is engineered to maximize numbers of clicks. And it points to sites that do not seem to provide anything else other than additional advertisments and promoted content.

Depending on the client, it might point towards other related content within that client's website or network. More often it seems to point towards content that is absurd, false, or otherwise meant almost exclusively to render clicks without regard for the quality, value, or existential merit of the target content.

<img class="blog-post" src="" alt=""/><figcaption></figcaption></figure>

Most notable are the images used for this content. They migth be titilating, provacative, bizarre, nightmarish, or otherwise completely unrelated to their titles.

<img class="blog-post" src="" alt=""/><figcaption></figcaption></figure>

The headlines are also pretty good:

[Examples]

### Why it's interesting

It's interesting because it's everywhere. It's interesting because it's engineered to be interesting. It's interesting because it's so extremely lowbrow, trashy, and it's absurd to believe that anyone would click on these links at all. Their analog is supermarket tabloids like the Weekly World News found in the checkout line.

<img class="blog-post" src="" alt=""/><figcaption></figcaption></figure>

Though why would this type of content be so ubiquitous if it didn't work? Proof that people actually do click on this content is evident in the simple fact that these content seem to be proliferating rapidly and anywhere that a content provider can't seem to advertise or build a subscription base otherwise. 

It is also potentially has a role to play in the recent phenomena of "fake news", which has had consequences far outside of its expectation simply to serve as a spot light for sponsored content on the web.  

Because I found it interesting and because it is not a trivial matter (anymore), I wanted to collect it. But I certainly did not want to waste my time browsing the internet manually to gather these bits of content. So I needed to have a process that would browse the internet for me and collect these absurd nuggest of information. 

### The collection process

1. I ran ()[a script using headless PhantomJS and Selenium as a driver] that scraped about 20 selected US websites (see list here) with known "suggested content" on them once every 7 hours for about 60 days. The more absurd, the better. Also, I tried to select a diversity of editorial perspectives across these sites. I wanted a sampling of sites that had different political views o see if there was any correclation between the political inclinations of the site producers and the content that appeared via third parties (i.e., would the native content on each site support, more or less, the same political agenda, where applicable?) 

2. On any given capture, I tried to avoid duplicates (defined by checking the headline of the content and the site it came from, to ensure we only got one of each unique piece of promoted content per site per scrape). But I left duplicates across different scrapes (or harvestings() as there might be good information about frequency of a certain piece of content such as which content appeared the most across multiple sites and scrapes.

3. Finally, I wanted to make the resource available to others (for research?) e.g., what content comes up at what times (correlation with news stories?)[1]

### Why?

It is possible that we could learn something about about how these services work by laying out a large number of their products in a searchable database and analyzing them for patterns. I also wanted to explore the connection between types of websites and the types of ads that were served up (e.g., which sites had more quasi-true ads as opposed to others). Finally, I wanted the longitudinal view. That is, to see which ads came and went, for how long, and in what intensities. Also could the same headline be applied to a number of different images or vice versa the same image applied to many different headlines?

That analysis is forthcoming...

### Some main challenges:

The final purpose of this post is to catalog some of the difficulties in gathering this content. Primarily, it is evidence that the web is still not a great API. Because the scraper relies on pulling top n articles and then scraping the third party content from a sampling of those, it will stop working for sites where the layout has changed. Or they might drop an ad content provider. All of these things might be tested for and logged properly. But to some extent, it's not worth that much effort for an experiment like this.

Sometimes they change their marketing strategy and the site begins to show the user overlays (subscribe to get this content, additional ads that users have to click off of to get to site content, etc.)

In many ways PhantomJS is great, but it still has a few issues. Namely that it fails or suceed inconsistenly depending where it is run from and what version you are using. I found that even though I had it running quite well and reliably on my laptop (with OSX), it was much less reliable when run on an Ubuntu server running the exact same version of everything in the script. 

It had a much less greater rate of success scraping native ad content from the article pages on th Ubuntu setup than on the mac setup (hovering around dropping 50% of pages on the former most likely on account of the third party javascript not loading up properly before attempting to scrape -- no matter how long it was set to wait before scraping). It is not clear why this was the case, and I think after a bit of troubleshooting, I just get the sense that PhantomJS is trying to do some complicated stuff, and can't be relied on to give a consistent headless browser experience across the board. 

For the purposes of this experiment, the workaround just forced the scraper to grab more than it probably would be able to properly ingest, in the hopes that it's yield scrape for scrape would be sufficient for a longitudinal analysis even though it errored out on half of the attempts it made every pass.


### Where to next?

With a good sampling of promoted content from different domains, sites with different political inclinations (or none at all), and over time, we might pursue some of the following:

- Understand content on a site per site basis or across sites?
- Image analysis, are these images in possession of some clickbaitability? What happens if we incorporate a nueral network to ___?
- Plumbing the evil depths (what happens when you get robots to click on the clicks)
- Analyze how these services differ between each other and how they themselves change over time
- Develop an "ontology" of suggested content
- Perform topic modeling, language analaysis, and perhaps use as the basis for generating artificial image and headline pairs.

So stay tuned for part 2. In the meantime, you can preview the analysis here: ____. And the data, refreshed nightly, may be accessed here.


### Notes
<section id="notes"/>
<b>[1]</b> I should not here that it was not until 30 days into the experiment that I remembered to collect also the specific news article from which a set of content items were pulled. So the data by that dimension is not entirely complete. [<a href="#back_1">back</a>]

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

