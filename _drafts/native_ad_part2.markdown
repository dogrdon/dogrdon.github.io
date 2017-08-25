---
layout: post
title: "Introduction to Internet Marketing Content Studies Pt. 2: Native Ad data is not as exciting as one would think"
description: "In a the last post, I detailed the motivation, approach, and challenges of collecting native advertising or suggested content on popular websites. In this post I explore the data collected and conclude with some remarks on observations, potential insights, and problems or shortcomings involved. Ultimately this remains an experiment and will not longer be pursued. The data can be accessed by others if they might be interested"
category: web
tags: [native ad networks, suggested content, spam, data analysis, web archiving, pandas]
---

<figure>
<img class="blog-post" src="" alt=""/><figcaption></figcaption>
</figure>

### Recap

Last month I finished pulling ads from across the web. You can see the process [here](link). While the data were not collecting in a scientific fashion, I still wanted to take the opportunity to explore it a bit and see what we'd gathered.

[Some prelimninary questions]

### Exploratory Analysis

Things to review: 

- Some common items like common headlines, group by political affiliation and explore trends there
	- Hint, there really aren't any.
- Explore trends over time
	- Data collected poorly, so probably nothing interesting.
- Do some image exploration 
    - Common image patterns - classify by a few buckets (gross, adult, food, person, car/plane)
    	- I am not doing this
    - Which types of images happen most on which types of sites
    	- Again, nothing really to see here


<figure>
<img class="blog-post-sm" src="" alt=""/>
<figcaption><a href=""></a></figcaption></figure>


### See for yourself

[Here](link to data)
[Here](link to notebook if you're curious-though you probably are not.)

### Conclusion

- Since data collection here was so stop and go and evolved over time, the results above are pretty unscientific.
- Since the data collection was so poor, any trends in the data are crowded out by inconsistent or overly redundant data collection
- The most compelling piece was the images, but what to do with that?
- Could go deeper with political affiliation, but perhaps that might be a bit of a fishing expedition. One I am no longer up for with this project
- Could have done more with timeseries, but collection was so inconsistent for many reasons
    - for some reason main scraper could not reach revcontent ads, so had to supplement
    - using proxies did not work
    - changing servers did not work
    - using headless chrome did not work

Overall, this was kind of a rat hole of a project. It was valuable to learn a little bit more about headless scrapers and native advertising in general, but getting any kind of signal out of this information has gone on a lot longer than I anticipated and in the end started to feel like squeezing blood from a turnip. So I am laying this one to rest. 




### Notes
<section id="notes"/>
<b>[1]</b> [<a href="#back_1">back</a>]

<b>[2]</b> [<a href="#back_2">back</a>]

