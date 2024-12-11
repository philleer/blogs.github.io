---
layout: default
title: "My Blog"
---

## NEWEST ARTICLES

## Featured Pages

{% for page in site.pages %}
  {% if page.name == "index.md" or page.name == "about.md" %}
    <h2><a href="{{ page.url }}">{{ page.title }}</a></h2>
    <p>{{ page.excerpt }}</p>
  {% endif %}
{% endfor %}


## Resume Files

{% assign resume_files = site.static_files | where: "path", "/resume/README.md" %}
{% for file in resume_files %}
  <h2><a href="{{ file.path }}">{{ file.name }}</a></h2>
{% endfor %}
