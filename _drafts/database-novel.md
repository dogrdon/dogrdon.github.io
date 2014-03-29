---
layout: project_post
title: "The Database Novel"
description: "A post detailing the novel as relational model"
category: project
tags: [writing, literature, georges perec, novel, puzzle]
image: 
---
{% include JB/setup %}

Before picking up Georges Perec's <a href="http://en.wikipedia.org/wiki/Life_A_User's_Manual" target="_blank">Life A User's Manual</a>, it had not occurred to me that a novel could be, in essense, structured data. 

Or rather, it might have occurred to me in the sense that books comprise a few predictable units, situated together: words make paragraphs, paragraphs make chapters, chapters comprise sections or parts (optional) and parts align to make an entire book. But it had not occurred to me that the elements of a novel, its content, the situations and items that inspire the plot or narrative might assemble as if a relational database or a conventional data structure. 

<img class="blog-post" src="http://longstreet.typepad.com/.a/6a00d83542d51e69e20128760d40a1970c-pi" alt="novel or story visualized as a data tree" title="story as structured data, borrowed from stackoverflow" />

Or such is the sense I get when reviewing the wikipedia <a href="http://en.wikipedia.org/wiki/Life_A_User's_Manual#The_constraints"> section </a> for this novel describing the constraints Perec used to craft his work.

<blockquote><b>The constraints</b>
These elements come together with Perec's constraints for the book (in keeping with Oulipo objectives): he created a complex system which would generate for each chapter a list of items, references or objects which that chapter should then contain or allude to. He described this system as a "machine for inspiring stories".

There are 42 lists of 10 objects each, gathered into 10 groups of 4 with the last two lists a special "Couples" list. Some examples:

<ul>
<li>number of people involved</li>
<li>length of the chapter in pages</li>
<li>an activity</li>
<li>a position of the body</li>
<li>emotions</li>
<li>an animal</li>
<li>reading material</li>
<li>countries</li>
<li>2 lists of novelists, from whom a literary quotation is required</li>
<li>"Couples", e.g. Pride and Prejudice, Laurel and Hardy.</li>
</ul>
</blockquote>

As I read this book, I am reminded how modular it is. It is the story of a Paris building on one day. And each chapter explores a single apartment in the building at a time, taking in the history of it's owners and their own personal relation, somehow, to the main character, Bartleby, an explorer and puzzle maker. 

Throughtout these stories, I often find it hard to follow a plot as each chapter seems to fixate more on the details of objects and objects are overwhelming the focus of attention and the glue that pulls together quick snaps of history and the interactions between residents: a list, a recipe, a sign on a door, a section of a catalog. 

The question creeps up to me: is it possible to write a novel first as if filling out a spreadsheet or set of form fields? To conceive of the objects necessary for a plot, assign them numbers, hierarchies, and a taxonomic spot in line from which to create a presentation from and <em> then </em> write the book?

I am imagining a relational database:

<img class='blog-post'  src='https://wiki.duraspace.org/download/attachments/32473993/DSpace-1.8-Database-Schema.png?version=1&amp;modificationDate=1366279060281&amp;api=v2' alt='image of a relational database model' title='relational database model'>

I am imagining that one might 'query' for the plot, or the interaction between characters, or some plot arc:

{%highlight sql%}

SELECT c.dialogue, c.action, c.conflict, p.scenario, p.context 
FROM characters c, plot p
LEFT JOIN observations ON observations.author_influence = c.author_influence
WHERE c.status = 'NOT DEAD' OR c.status = 'MYSTERIOUS'

{%endhighlight%}

Silly as it sounds, it might make for an interesting project in language processing. Would anyone read it as they do <a href="http://en.wikipedia.org/wiki/Finnegans_Wake">Finnegan's Wake</a>? Trying to locate somekind of meaning in the incidental writing?



