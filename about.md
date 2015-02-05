---
layout: page
title: About
permalink: /about/
---

Frank joined [minubo](http://www.minubo.com) in 2013 as one of their first engineering hires. He ensures IT operations run smoothly and advocates agile workflows throughout the company.

### Contact me

[frank.langanke@googlemail.com](mailto:frank.langanke@googlemail.com)

{% assign pages = site.pages | sort:"weight"  %}
<ul>
  {% for p in pages %}
    <li>
      <a {% if p.url == page.url %}class="active"{% endif %} href="{{ p.url }}">
        {{ p.title }}
      </a>
    </li>
  {% endfor %}
</ul>

