---
layout: archive
permalink: /machine-learning/
title: "Machine Learning Projects"
author_profile: true
header:
  image: "/images/book12.jpeg"
  
---

# 1. Engagement Test (A/ B Test)

* Description of Data:
The compnay of this project is a social network. They decide to add a feature called: Recommand Friends, i.e sugget people you may know on the user newsfeed. A model has built to suggest 5 people to each user. The test has been running for some time, we wamt to check for each user, the number of pages visited during their first session since the test started. If this number increased, the test is a success.

* Research questions:
This project aims to check A/B test result to test whether new feature has positive effect on
engagement. And identify the test performance on different user segments.
1. Perform A/B test
2. Look at actionable insights to improve engagement


* Analyses to answer research questions:

  We first look at the data set, clean it and merge two tables.

```{r}
data=merge(test,user,by="user_id", all.x=TRUE)
summary(data)
str(data)
```
---
![](/images/AB1.png) 

---










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
