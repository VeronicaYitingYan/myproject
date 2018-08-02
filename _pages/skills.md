
---
layout: archive
permalink: /skills/
title: "skills"
author_profile: true
header:
  images:"/images/book7.jpg"
---

{% include base_path %}
{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}

Tool - Python, R, SQL, VBA, Linux
Language – Django, Postgresql, NoSql, Mongodb, Amazon Web Services
Data Science – A/B Test, Random Forest, Logistic Regression, Decision Tree, KNN, Cluster
Visualization – PowerBI
