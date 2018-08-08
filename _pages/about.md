---
layout: archive
permalink: /about/
title: "About"
author_profile: true
header:
  image: "/images/book23.png"
---

Goal-oriented data scientist with 3+  years of experience in building decision support models for product line in Electronic Engineering and Insurance area. Strong skills in Statistics, Mathematical Analysis, Machine Learning, Data ETL (extract, transform and load) and Data Mining. A self-motivated and competent individual who are passionate about Data.
  

{% include base_path %}
{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}
