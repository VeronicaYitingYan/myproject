---
layout: archive
permalink: /machine-learning/
title: "Machine Learning Post by Tags"
author_profile: true
header:
  image: "/images/book6.jpg"
  
---



Engagement Test (A/ B Test)

Tested whether new feature has positive effect on engagement
Analyzed actionable insights to improve engagement
Performed Novelty Effect analysis for feature evaluation by tracking the behaviors of new and old users. 


Random Forest on CTR   

Performed basic feature engineering
Built Random Forest model to improve email campaign result 
Extracted insights from the model via partial dependence plots



{% include base_path %}
{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}
