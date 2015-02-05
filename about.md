---
layout: page
title: About
permalink: /about/
---

Frank joined [minubo](http://www.minubo.com) in 2013 as one of their first engineering hires. He ensures IT operations run smoothly and advocates agile workflows throughout the company.

### Contact me

[frank.langanke@googlemail.com](mailto:frank.langanke@googlemail.com)

{% for post in site.posts %}	
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <p><small><strong>{{ post.date | date: "%B %e, %Y" }}</strong> . {{ post.category }} . <a href="http://erjjones.github.com{{ post.url }}#disqus_thread"></a></small></p>			
{% endfor %}	

