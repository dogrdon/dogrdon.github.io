---
layout: post
title: "Recommended Content on the Web Pt. 1: The Web is not an API"
description: "Suggested content on the web, often ignored or blocked, is both ubiquitous and invisible. Information can take on a different value when aggregated and presented outside of its original context. This post details how I originally sought to take on the collection, analysis, and showcasing those clickbait, suggested content articles that accompany most commercial, high traffic web sites. What I found out is how fragile, bloated, and unpredictable the web is and how it is not anything close to an API if you seek to handle its content like structured data."
category: web
tags: [native ad networks, suggested content, spam, data analysis, web archiving]
---

<figure>
<img class="blog-post" src="" alt=""/><figcaption></figcaption></figure>

### What is it?

Suggestions from native ad networks like Taboola, Outbrain, Revcontent, Content.Ad, Adblade, AdsWift, SiteAd, ContentDing (I've made up a couple) often serve the purpose of connecting site users with articles or 'content' on other web domains. They are generally found bundled up in rows of three somewhere around the end of the article and the comments section. These services operate by providing their clients a source of ad revenue. And so the content is engineered to maximize numbers of clicks.

The content is often arbitrary, false, or otherwise meant almost exclusively to render clicks without regard for the quality, value, or existential merit of the target content.

More notable are the images used for this content. The can be titilating, bizarre, nightmarish, or otherwise completely unrelated to their titles.

[Examples]

[How does this stuff actually work?] 

### Why it's interesting

It's interesting because it's everywhere. It's interesting because it's engineered to be interesting. It's interesting because it's so extremely lowbrow, and it facinates me that anyone would click on these links at all (anyone who has ever done so should have learned their lesson). Proof that people actually do click on this content is evident in the simple fact that these content seem to be proliferating rapidly.  

Therefore, I wanted to collect it. And to do so I needed to have a process that would browse the internet for me and collect these absurd nuggest of information.


### What did I do?

1. scraped selected websites with know "suggested content" on them for 30 days, the more absurd, the better
2. On any given capture made sure to avoid duplicates (defined by: ), but left duplicates across harvestings as there might be good information about frequency of a certain link. Of course they could also be more widely deduped later.
3. Wanted to make the resource available to others (for research?) e.g., what content comes up at what times (correlation with news stories?)

### Why?

Well, it's possible that we could learn something about about how these services work by laying out a large number of their products in a searchable database. Also wanted to explore the connection between types of websites and the types of ads that were served up (e.g., which sites had more quasi-true ads as opposed to others). Finally, I wanted the longitudinal view. That is, to see which ads came and went, for how long, and in what intensities. Also could the same headline be applied to a number of differen images or vice versa the same image applied to many different headlines.

- Understand content on a site per site basis or across sites?
- Image analysis, are these images in possession of some clickbaitability?
- Plumbing the evil depths (what happens when you get robots to click on the clicks)
- capture cookie information as part of the SIP
- would want to analyze how these services differ between each other and how they themselves change over time
- ontology of suggested content
- how it makes web pages bloated (way to visualize)


### Some main challenges:

- The web is still not a good API, and content does not abide by much of a standard (the web is shit), "content" is destroying our chances at this. Sometimes there's just too much going on: overlays...
- PhantomJS is great, but has issues. Namely that it might fail or suceed inconsistenly. I found that even though I had it running quite well and reliably on my laptop (with OSX), it was much less reliable when run on an Ubuntu server running the exact same version of everything in the script.
- Sites and content providers are finicky, they change their layout, they change native ad services regularly. It's hard to keep up with it.

### Where to next?

#### PRESENTATION, INVITING OTHERS
- An exhibit resource (gallery) drawing connections btw items. Ways to grab subjects or topic modeling for things (food, celebrities, health, crime, sex, sex)
- A microcosm of the internet itself, the extreme end if "content". This is the distilled result of these companies best guess of what will draw attention.
- "As a discourse, it's watching machines and reptilian minded marketing initiatives talking to sometime the interests of a specific user (cookies) or perhaps the basest desires of a composite sketch of your average web user."
- probably have a little bit of analysis on what is already there (PT.2)
- provide access to data





### Notes
<section id="notes"/>
<b>[1]</b> [<a href="#back_1">back</a>]

<b>[2]</b> [<a href="#back_2">back</a>]




TOINCLUDE
=========


#### Bibliography


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

