---
layout: page
title: About
---
<br>
*This is HarryYu31's blog*
<br>
Hello there! This is a website about all sorts of weird projects I do, just for fun though, nothing serious
-----

# Links to projects:
{% assign postsByYearMonth = site.posts | group_by_exp: "post", "post.date | date: '%B %Y'" %}
{% for yearMonth in postsByYearMonth %}
  <h2>{{ yearMonth.name }}</h2>
  <ul>
    {% for post in yearMonth.items %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}



<br><br><br><br><br>*Still under construction...*<br><br><br>
