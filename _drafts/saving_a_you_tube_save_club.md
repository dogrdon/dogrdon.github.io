---
layout: post
title: "Saving Stupid Videos: Preserving YouTube and why can't we preserve the Internet ourselves."
description: "Attempting to preserve a small, intimate piece of the Internet shows the threadbare future of keeping digital content beyond a few years from now."
category: digital-libraries
tags: [preservation, access, archives, the web, personal, video, favorites]
---
{% include JB/setup %}

1. 

At the end of last month, I had the priviledge of attending the Personal Digital Archiving Conference in New York. I came away from it wanting to revisit a small project I had long set aside. The process of pushing it through to completion got me thinking more about what it means to select, share, and save somethign on the Internet. 

Sometime around 2008 - 2009, a few friends and I used a single YouTube account for sharing videos between ourselves. Mainly silly stuff, some of which were some of the big meme's or viral videos of the moment (It's gonna be hot...), some of which were obscure music videos, and most of which were just kind of funny or interesting. Nothing too serious, nothing too educational. Primarily it was content that we used to communicate our sense of humor with eachother. But this was a YouTube playlist, and we would just login with a shared password ('password') and add videos that we thought belonged there. A sort of asynchronous version of the sitting around and watching funny YouTube videos together. And so it wasn't even our content, though sharing it in this closed circle, without making a big show of it, I imagine this is what it might have felt like to watch home movies (a common trope in terms of nostalgia) in a private setting. 

What made this special, I suppose, is that it wasn't the intended way we are supposed to share digital media online. Though most of those tools for sharing tend to just generate more noise. Share on Facebook, Twitter, other social media sites, or on e-mail and sure it would get around and be watched. But it would quickly disappear as it streams off into the chaos of your news feed, or stream, or the archive of your inbox. In our case, though, each video was listed right after the last one, and they always retained their order. And through this a quasi-dialog would emerge. And after many weeks or months, the record of these selections were still intact. And I could wax on and on about how valuable to us this was, but the more important thing here is how it disappeared and came back. 

In 2010 I made the decision to delete the YouTube account as I was trying to do a little house keeping of my profile (it was my account, after all). But before deleting, I saved a copy of the playlist by simply saving the HTML list from the browser. Not a great way to preserve anything on the Internet. After a while, I got an email from one of my friends asking what happened to it. I said it's gone, but I kept the HTML, and maybe I could go back and download the clips, but that never happened. 

Coming off of the conference, I wanted to bring the list back. I had all the HTML, after all. So I scraped that out and put that into a small database (154 vides in total). From there I had titles, original links, the order in which they were added to the original playlist, the user who uploaded it, and the duration of the clip. Using a python module called Pafy, I could then automatically check and see which of the videos were still there and which had removed (or made private). Surprisingly, after almost 5 years, out of the 154 original, 116 were still up, and 38 had been taken offline. 

I spent a little time manually checking for replacements and whether the original user was still around and found that I could reasonably replace 23, while about 15 seemed to be gone for good (based on video duration, memory of the clip, and the title). Often the reason why a video could not be replaced was because it was something of which many different versions existed and I could not be too sure which one we had uploaded (it makes a difference, a rare live version or music video of a popular song is not the same as a fan tribute with a photo gallery of the artist). With most of the videos now accounted for, I could repopulate a new playlist and put the "collection" back online.

Though it's interesting to note the fate of some of the lost videos:
	- 10 accounts removed for multiple copyright violations
	- 4 copyright blocks on the content
	- 2 accounts terminated
	- 1 video in violation of YT terms of service
	- 3 videos private and
	- 18 videos marked simply as unavailable (sorry)
	- 11 users deleted because of multiple copyright claims
	- 2 users deleted because of repeated or sever violations and or copyright claims
	- 18 users are still live (or at least the usernames are - not sure how much this has to do with YouTubes decision to drop vanity URLs for everyone)
	- 7 users just do not exist anymore

Often it is copyright claims that take videos off of YouTube.

From there, I felt that it was important to take the step of downloading these clips to my computer along with the metadata, and store those in two different locations, in the event that any of the videos do go down and become unavailable. 

Challenge 1: It is against YouTube's TOS to download videos. I realize that, though I am not doing so for any purpose other than to ensure my own personal enjoyment into the future.

Challenge 2: YouTube offeres the ability to download and archive your own uploaded content (in the original upload formats, as well), but for the reasons that we do not own other people's content, we can not download it, even if it is our intent to continue to provide access to that content in the future. 

Accordingly, YouTube is not necessarily built with preservation in mind. Nor should it be. But I think what I'd like to argue here is that maybe there is a case for developing the client-side tools for users to engage in their own preservation of online content. 

Lessons learned...

- a bit of a preamble: this is not preservation in the professional sense. This is more like backing up. But I think what's important to emphasize here is that this is also not related to backing up one's own uploads and work. That's a solution that Google already provides [takeout]. But what about the interaction, culture importance of a selection of videos. A curated list of videos, these are well more fragile and ephemeral because they draw from a number of creators, quickly a playlist can become shot through with copyright infringement takedowns, closed accounts, so on and so forth. There is also an ephemerality to videos that were not put up with much effort, loss or no metadat to begin with, shoddy titles. But the work underneath still points at something, conveys some meaning, and having found it under the rubble is a bit of an accomplishment. How do we somehow save these moments, with as much context and understandability as is allowed by the original upload?

- it's not the original files, of course, this is a cheap proxy. 
- but these videos truly gain more importance by being selected and placed in relation to other videos (the basis of curation)

But so what, right? What do a few silly meme videos, popular jokes, and obscure video clips have to do with preservation, or the future of digital content on the Internet?

Conclusions
- Some examples have been provided here with backups found elsewhere. Though I cannot garuantee that even these measures will ensure preservation. Though I do think that when it comes to matters of digital preservation, we can't wait for the digital content platforms or even the institutions that have digital preservation as a mission to support the saving of our cultural artifacts. Specifically the ones that lack political and historical power. The ephemera will get lost, as it usually does. But with the web we can begin to take a stance on preservation of the things we like the most. And hope that the infrastructure comes around that not only helps us collect digital media, but to preserve if for later enjoyment and the narration of our selves (or whatever)

- and this leads me to a bigger point, which gets at the nature of preserving content on the internet more globally. It's not going to be feasible for centralized entities to preserve the internet, or at least it's not feasible to think they can do it alone. It is not new to think that the digital preservation strategy for digital content on the Internet will have to be more distributed. And even distributed efforts by institutions will fail because they will have to collect for a purpose or lose context. As seen here, a small collection of videos gain their meaning through a very local and particular context. And for that, it is not a collecion that has mass appeal. But the consequence of it is more preservation. There is more preserved now than was preserved without action. What I mean to say then is that digital preservation strategies for the Internet need to allow for the contributions of non-archivists. And this can be done by building easy to use tools for preservation into the web itself. It is not enough to preserve one's own content (many componies now allow you to export an archive of your own content). But what if someone identifies and at risk Tumblr (hasn't been updated in a while, it may be abandoned though at one point it produced a lot of interesting and relevant original content). Other users should have the tools available in some fashion to flag content for saving (rather than just flagging for deletion). It's a broad step in another direction than we are used to thinking of the web. But when content changes so drastically, we begin to notice the ephemerality of much of this content over a very short period of time. One might also argue that these steps are checks against corporate domination of the web (and why things like Diaspora are not failed projects, just ahead of their time or outside of the predominate business model that serves as the current organizing principle of the web).


NOTES:

* saving a bunch of youtube faves from 2008 - 2009 and destroyed in 2010?
* evidence of what exists, rebuilding it
* significance they had of a shared curation of youtube videos
* how many remain,
* what happened to the others, an analysis.
* the act of favoriting things
* cultural memory
* trying to salvage a practice between people
* others do this, maybe not in this manner
* using social media as a place to store emotions and memories you don't have time to process now
* I can't perform in public,
* favoriting and passive social media as a practice, a cultural practice
* synthesize quick and move on
* context of watching
* twitter is not my favorite, but every now and again it's useful/helpul

What, 
	- 154 videos total, 
	- 116 still up, 
	- 38 down

	- after remediation: 23 videos could be recovered while 15 appear to be lost to the ages
		for a number of reasons:
			- not enough details, very vague or unspecific metadata
			- many copies of something similar, but decidedly not the original either by memory or because length of video
			- some interesting phenomena. B4-4 Get Down appears to be widely mocked, but there is no unadulterated remaining copy of the video (some joker on vimeo introducing it). It is available, but not in this country. I would hate to be that legal team.
			- 10 accounts removed for multiple copyright violations
			- 4 copyright blocks on the content
			- 2 accounts terminated
			- 1 video in violation of YT terms of service
			- 3 videos private and
			- 18 videos marked simply as unavailable (sorry)
			- 11 users deleted because of multiple copyright claims
			- 2 users deleted because of repeated or sever violations and or copyright claims
			- 18 users are still live (or at least the usernames are)
			- 7 users just do not exist

	- when to download, 
	- when to update metadata, 
	- what implications for other uses, 
	- what ideas for monitoring/protecting youtube uploads from going away?
	- what workflows for protecting youtube videos once you've shared/favorited or otherwise marked it.

Next steps, 
	- separate the available from the unavailable
	- go find out if there is another copy of the unavailable
	- go find out what happened to the user
	- enter the new vid and user disposition into the database
	- download all videos
	- resurrect the youtube channel
	- create a check for the playlist itself (or the database)
		- make sure all vids are still available
		- mark any that have become unavailable
		- normalize?
		- clean up and keep checking
		- what to do about things that have gotten lost between checks?