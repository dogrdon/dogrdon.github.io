---
layout: post
title: "Saving Stupid Videos: Preserving YouTube"
description: "Attempting to preserve a small, intimate piece of the Internet shows the threadbare future of keeping digital content beyond a few years from now."
category: digital-libraries
tags: [digital preservation, access, archives, personal, digital ephemera, video]
---
{% include JB/setup %}

<div class="figure">
<img class="blog-post" src="/assets/images/posts/2015/05/yt-unavailable-sorry.png" alt="Image of YouTube video when the video is unavailable (sorry)"/><div class="figcaption">Sorry, indeed.</div></div>

####The Setup

At the end of last month, I had the privilege of attending the [Personal Digital Archiving Conference](http://personaldigitalarchiving.com/){:target="_blank"} in New York. I came away from it wanting to revisit a small project I had long set aside. The process of pushing that through to some semblance of completion got me thinking more about what it means to select, share, and preserve stuff on the Internet. 

Sometime around 2008 - 2009, a few friends and I used a single YouTube account for sharing videos between ourselves. Mainly silly, viral stuff ([cats and dogs sounding like they are speaking English](https://www.youtube.com/watch?v=eV71mpbvl-g){:target="_blank"}), inside jokes ([earnest recordings of alpaca walking towards a camera](https://www.youtube.com/watch?v=GP5D2apU2SE){:target="_blank"}), ironically amusing advertisements from the 80s, or just things we wanted to show to each other ([Gregory Corso talking about Jack Kerouac](https://www.youtube.com/watch?v=1z1LkYLDCrg){:target="_blank"}, [Cerrone's video for Supernature](https://www.youtube.com/watch?v=QgGK4qBTwpw){:target="_blank"}). We shared them because they were funny, ridiculous, or cool, or what we considered rare-finds, but more importantly I think we shared them because they contained valuable information about things we had a shared interest in.

As a resource, it was a single YouTube playlist and we would just log in with a shared, easy to remember password ('password') and added videos that we thought belonged there. It was a sort of asynchronous version of the act of gathering together and watching clips. It was not our content, though sharing it in this closed circle, without making a big show of it on wide broadcast social media streams, I imagine this was the next best thing to watching home movies in a private setting. In a sense we also added our own personal memories on top of this content by rounding it up in this fashion. By going back over it, it is an aid to remembering what in our own lives each video might have been a reference to at the time.

One reason why I think this is all worth noting is that this isn't the intended way we are supposed to share digital media online. Most of those tools available for sharing tend to generate more noise than community. They encourage us to share on Facebook, on Twitter, or any other number of social media applications, or through e-mail. And through those channels it quickly circulates, and is done so, often, under the scrutiny of your friends' friends. Shared in that fashion, it is just as quickly buried under the chaos of ones news feed, or stream, or inbox archive. 

In this case, though, each video was reliably listed in the order they were shared, all in one page. You could visit whenever you wanted and the items selected would not be drowned out by the countless other pieces of information you have had pushed upon you by your circle of friends and acquaintances. It's passive, sure. But it was effective for curating content for a very specific audience. Through this effort a quasi-dialog would emerge. After many weeks or months, the record of these selections were still intact. After much longer, it can show you how much or how little your tastes might have changed. 

####The Plot Thickens

In 2010 I made the decision to delete the YouTube account in an attempt to clean up my profile online. But before deleting, I retained a copy of the playlist by simply clicking "Save As..." from the browser. Not a great way to preserve anything on the Internet, but it was sufficient. After a while, I got an email from one of my friends asking what happened to the list. I told them it was gone, but I sent along the HTML file, and said maybe I could go back and download the clips, but that never happened. 

Coming out of the conference, I wanted to bring the list back. I scraped out the necessary information from the saved HTML file and put that into a small database (154 videos in total). From that I had titles, original links (and a YouTube asset ID), the order in which they were added to the original playlist, the user who uploaded the video, and the duration of the clip. Using a python library called [Pafy](https://github.com/np1/pafy), I could then automatically check and see which of the videos were still there and which had been removed (or made private). Surprisingly, after almost 5 years, out of the 154 original videos in the playlist, 116 were still up, while 38 had been taken offline. 

I spent a little time manually checking for replacements and whether the original user was still around and found that I could reasonably replace 23 videos (based on duration, memory of what the clip contained, and the title), while about 15 videos seemed to be gone for good. Often the reason why a video could not be replaced was because it was something of which there were many different versions and I could not be too sure which one we had added (e.g. the difference between a rare live version of a song and a user made photo collage to accompany that song). With most of the videos now accounted for, I could repopulate a new playlist and put the "collection" back online.

Though it's interesting to note the fate of some of the lost videos and accounts:

	- 10 accounts had been removed for multiple copyright violations
	- 1 video was in violation of YouTube terms of service and/or copyright violation
	- 3 videos had been marked private
	- 18 videos were marked simply as unavailable 
	- 4 videos had been removed because of copyright blocks
	- 2 had been accounts terminated because of repeated or severe violations and or copyright claims
	- 18 users, though, were still live, but the content of interest had been removed
	- 7 users just did not exist anymore on YouTube

Not surprisingly, copyright claims appear to be a front-running problem for the preservation of YouTube content.

From there, I felt that it was important to take the step of downloading these clips and organizing them on my local drive along with the metadata (again, using Pafy), and storing all that in two different locations (three, actually: my laptop, my laptop's backup drive, and Dropbox). In the event that any of the videos do go down or become unavailable, there is a copy somewhere such that the collection should always, theoretically, remain whole. Though there are a few problems preserving anything on YouTube.

<b>Problem 1:</b> It is against YouTube's TOS ([Section 5, Subsection B.](https://www.youtube.com/static?template=terms){:target="_blank"}) to download videos in this fashion. I realize that. Though I am not doing so for any purpose other than to ensure my own personal enjoyment of these media into the future.

<b>Problem 2:</b> Where does one put this content for future access, and how should one store it? I have the videos now in a Dropbox account. Though what happens if Dropbox goes out of business? Additionally, while these videos are relatively small, larger video content is a pain to store as these files can get very large and occupy a lot of digital space. Finally, I have not gone through much of the effort of truly preserving these objects. I am not keeping administrative metadata, or provenance, for instance. Nor am I using any archival schema for keeping the metadata. It's just JSON packed along side its video. I have decided to at least create a md5 hash in the event of wanting to do any checksums in the future. But these are not preservation copies and so they're already a bit degraded by having been through whatever transcoding process YouTube does in addition to any disintegration of the original media well before uploading to YouTube. True preservation of this content might just be overkill.

What is obvious to me now (though should not come as any surprise) is that YouTube is not really built with preservation in mind. Nor do I think it should be. But I think what I'd like to argue here is that maybe there is a case for developing the client-side tools for users to engage in their own preservation of online content. Allowing users to make decisions about storing content for safe keeping (and access) beyond the inevitable expiration date of these media might be a part of the solution to the explosion of digital content on a platform that does not prioritize long-term persistence. Though what that looks like is not certain. Additionally, the very copyright regulations that bring down content from places like YouTube in the first place would be a non-starter for any such tools being built by these companies in the first place.

####What it all means

But so what, right? What do a few silly and obscure video clips at low resolution have to do with preservation, or the future of digital content on the Internet?

In [his talk at the 2013 National Digital Forum](http://inkdroid.org/journal/2013/11/26/the-web-as-a-preservation-medium/){:target="_blank"}, Ed Summers discusses the importance of nurturing more collaborative, decentralized models for preservation that allow users to capture parts of the web in small, localized batches. In that vein, he writes: "We need best practices, or really just patterns for creating HTML packages of archival content. We need to make sure our work sits on top of common tools for the Web." By which I understand that there needs to be the tools for preserving the content of today in the hands of more than just the institutions and the archival professionals. 

As mentioned, what I have here is not preservation by a long stretch. It is certainly not web preservation. For the most part, I am not even interested in keeping track of anything more than the assets and some basic metadata for those videos. I've chosen to completely disregard the code that makes a YouTube page function. Again, the saved files are transcoded copies meant for web streaming. They are a cheap proxy of the original upload (which users themselves can download through Google's [takeout service](https://www.google.com/settings/takeout){:target="_blank"}). My approach was more like backing up a derivative access copy than archiving. 

But it's important to emphasize again that this is not backing up my own digital content. It's saving other peoples content that has been fashioned into a particular order (like an exhibit), for a limited audience. That is, there are very few people outside a small circle of friends that are interested in the persistence of this content. It's about saving content that has been removed from its original content and placed in a new context. In a sense, it's also about preserving the post-modern process around content and not just content itself. 

But I can imagine that others might have similar collections of content that they have also found and shared with their friends in some context or another. We should all know instinctively by now that in placing objects together in different configurations, we can learn something new about them, or at the very least enjoy them and understand them in different ways. In such a way, any tools for preserving these collections would map to the distributed, networked, and fungible nature of the Internet itself. 

By virtue of being an assemblage of artifacts created by a vast number of different contributors, these collections are more fragile, more ephemeral because they could quickly be pulled apart by copyright infringement takedowns, closed accounts, videos made private, etc. There is also the matter of this ephemeral content being put up with minimal effort with respect to object description. It might lack metadata or have uninformative titles. It is cataloged via folksonomy, and not via controlled vocabularies. Yet the work underneath still points at meaning, conveys culture. So how do we save these packages, with as much context and understandability as is available via the original upload?

In light of this, we can't wait for the digital content platforms or the cultural heritage institutions to preserve our content (or the content of others) for us. These ephemera will get lost. It's not going to be feasible for centralized entities to preserve the Internet, or at least it's not feasible to think they can do it alone. 

In the end I want to say that it is not enough to allow for the preservation one's own content. But what if someone identifies an at risk YouTube account or Tumblr account (i.e. it hasn't been updated in a while, it may be abandoned though at one point it produced a lot of interesting and relevant original content). Sometimes we cannot rely on the original creators to be stewards of their own content (though in some cases - that is, where one might want to disavow their connection to any such content they might have put up - that might be intentional). Though in instances where it is done respectfully, and in the best interests of the creator and the community for which the creator posted, it might be beneficial for other users to have the tools available in some fashion to mark and actively process content for saving. It's a broad step in another direction than we are used to thinking of the web. But where content that impacts so many has such a potentially short life span, we might want to create mechanisms, embedded in the very fabric of the web we use daily, to stem the disintegration of that content and their relationship to other content. 


