---
layout: project_post
title: "Historical GIFs (AKA dpla.gif)"
description: "A twitter bot that pops into the Digital Public Library of America's collection of moving images and posts GIF image excerpts as it goes."
category: project 
comments: false
tags: [ffmpeg, ruby, video, GIF, mongodb]
image: /assets/images/projects/dpladotgif/hist_gif_sloth.gif
---

<p>In connecting to the <a href="http://dp.la/info/developers/codex/">Digital Public Library of America's API</a>, <a href="https://twitter.com/dpladotgif">Historical GIFs (@dpladotgif)</a> attempts to make visible the vast collection of moving images housed in America's libraries and archives. Sometimes the only way to know what is there is to see it.</p>

<p>Several times a day the bot grabs a word to search the DPLA and selects something from the results for the purpose of extracting a short GIF to post to twitter. Post outcomes are stored in a mongodb database to avoid repeats and provide for later analysis.</p>

<a class="source" href="https://github.com/dogrdon/accidentalculture">The code that powers this bot.</a>
