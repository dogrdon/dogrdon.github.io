---
layout: page
title: ![title](http://www.example.com)
tagline: 
category: home
---
{% include JB/setup %}

![spinning pentakisdodechahedron on wikipedia](http://upload.wikimedia.org/wikipedia/commons/f/fc/Pentakisdodecahedron02.gif "Spinning Pentakisdodecahedron")

<h2>Posts</h2>

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li><br/>
    <div class="post-description"><b>Summary:</b> {{ post.description }} <a href="{{ BASE_PATH }}{{ post.url }}"> <br />>>Go to post</a> </div><br/>
    <hr>
  {% endfor %}
</ul>



