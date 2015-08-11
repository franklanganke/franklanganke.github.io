---
layout: page
title: About Frank Langanke
permalink: /about/
---
*It Is Always About the People, Not Technology*

I am a Software Engineer from Hamburg with a strong focus on Java, Agile Principles, DevOps Culture and AWS. Since 2013 I am Head of IT Operations at [minubo](http://www.minubo.com), a big data tech startup, wearing many hats. Lead AWS engineer, release engineer, agile coach, team lead. 

Before minubo I worked as a technical consultant for different IT Services companies ([Prolifics](http://www.prolifics.com/), [NTT DATA](http://www.nttdata.com/)) mainly on enterprise projects for about 10 years. I am a graduate of the University of Hamburg (Business Informatics / Diplom-Wirtschaftsinformatik). 

### Contact me

[frank.langanke@googlemail.com](mailto:frank.langanke@googlemail.com)


### All Posts
{% assign pages = site.posts | sort:"weight"  %}
<ul>
  {% for p in pages %}
    <li>
      <a {% if p.url == page.url %}class="active"{% endif %} href="{{ p.url }}">
        {{ p.title }}
      </a>
    </li>
  {% endfor %}
</ul>

