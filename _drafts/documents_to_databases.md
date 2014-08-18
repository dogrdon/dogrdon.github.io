---
layout: post
title: "Documents to Databases - An exploration of turning digital documents into strucuted data"
description: "Often when working with data, one will be tasked with converting somewhat strcutured data into actually structured data. That is, one will need to convert a table or pattern formatted information in a word document or PDF into a database or flatfile datastore."
category: data
tags: [data]
---
{% include JB/setup %}

### The Problem

*It would seem that converting information in word docs to a more structured formate would be a 'solved problem' by now. It's a fairly common problem, it's a need that I can see many organizations having, and it does not seem like too unwieldy of a process: after all, word docs already have a structure to their formatting, it's just a matter of parsing that in a reliable way.

*I am coming to find that there are very few turn key solutions for handling word docs (to say nothing of PDFs). There are a few conversion tools <list them>, but a lot of them are desktop gui programs for word. I would like to see more Python or Ruby libraries that handle this sort of stuff seeing as how that is where I already see a lot of text processing utilities that can easily be brought into other open source projects that could use them. 

*The native conversion of word docs to XML is atrocious, leaves you with very verbose and messy XML

*We don't want to just extract text from a .doc|x file or read it, we want to essentially scrape it...or put it into a format that can be scraped.


### Potential Tools in the tool chain

*There is a word2cleanhtml web app that claims to use lxml, the python library for parsing XML, for most of its transformation. But that code is not open sourced.

*does lxml have native word doc handling capabilities?

*other ways for first converting word docs to a more traversable format like HTML or XML.

*difference between .doc and .docx files since docx is already XML based (though we don't yet know how clean it is till we look further into that standard)? If so, does it make sense to parse only .docx and so convert all doc to that first. [1]

*Parsing a docx document in its native XML format. You _can_ unzip a .docx file and you'll get a file at `./word/document.xml` which you may think you can parse. This is pretty much a joke, even if your document is predictably formatted, finding the reflection of this formating in your XML tree would be a massive headache. Feeding your docx file to a python-docx `Document` object gives you a change to parse on special characters and formating (like continous breaks) in a more reasonable fashion.

*python-docx - this library looks like it works mostly for the create of .docx files, but not the parsing and reading of them (for instance, only a few methods for reading text out of a table cell or paragraph, .text methods reserved for writing into the document) - though it kicks out text for paragraphs, but that's about as good as just copy pasting over to a text file.

*


[1]Some references for doc and docx parsing: 
	[1](http://stackoverflow.com/questions/14584747/parsing-a-doc-word-file-with-a-python-script-unix)
	[2](http://stackoverflow.com/questions/125222/extracting-text-from-ms-word-files-in-python)
	[3](http://stackoverflow.com/questions/4262903/best-way-to-process-a-word-document)
