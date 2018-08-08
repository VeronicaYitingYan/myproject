---   
layout: archive
permalink: /skills/
title: "Skills"
author_profile: true
header:
  image: "/images/book7.jpeg"
      
---

**Language** - Python, R, SQL, VBA, Linux <br/>
**Tool** – Django, Postgresql, NoSql, Mongodb, Amazon Web Services<br/>
**Data Science** – A/B Test, Random Forest, Logistic Regression, Decision Tree, KNN, Cluster<br/>
**Visualization** – PowerBI<br/>

{% include base_path %}
{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}
