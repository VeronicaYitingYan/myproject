---
title: " Engagement Test (A/ B Test)"
date: 2018-08-08
tags: [machine learning, data science, random forest]
header:
    image: "/images/book12.jpeg"
excerpt: "A/B Test, Engagement, Data Science"
mathjax: "true"

---


* Background:  

   It is a new feature test on a Social Network Company. They decide to add a feature called: Recommend Friends, i.e suggest people you may know on the user newsfeed. A model has built to suggest 5 people to each user. The test has been running for some time, we aims to test wether the new feature will increase the page visiting volume.

* Description of Data:   

   This data file has two tables, user_table and test_table. Company runs A/B test on a random subset of users. We want to check for each user, the number of pages visited during their first session since the test started.

* Research questions:  
   This project aims to check A/B test result to test whether new feature has positive effect on engagement. And identify the test performance on different user segments.   
      1. Perform A/B test
      2. Look at actionable insights to improve engagement


* Analyses to answer research questions:

  We first look at the data set, clean it and then merge two tables.

```r
library(rpart)
library(dplyr)
library(ggplot2)

data=merge(test,user,by="user_id", all.x=TRUE)
summary(data)
str(data)
```
<img src="{{ site.url }}{{ site.baseurl }}/images/AB1.png" alt="summary of data">

The average engagement is around 4.6. Data set looks good and no strange data point need to clean. Just noticed, “Opera” have much lower rate than browser methods, is there any reason?   
Simple t-test is considered here to do A/B test.

```r
t.test(data$pages_visited[data$test==1],data$pages_visited[data$test==0])
```
<img src="{{ site.url }}{{ site.baseurl }}/images/ttest.png">

P-value is 0.5775, large than 0.05 significant level. We are not be able to reject the null hypothesis that there is no difference between these two groups.

In average, every user in control group visits 4.6 pages while test group with new feature is 4.5997. Test group slightly worse than control group. It is against our expectation. Does the new feature really bad? Or any bias of data set?

Look at test/control ration over time. There is no evidence shows test group consistently performs worse than control group. Also, small variance indicates we collected enough data. Maybe, there is bias in data collection.

<img src="{{ site.url }}{{ site.baseurl }}/images/ratio.png">

We check the bias by building a tree with “maxdepth=2”. If the data in test group and control group have same distribution, tree will not split at all.
The result is interesting, tree split at “browser”. The leaf with average page visit is 4.6. Random is perfect on one side of the split (browser=Chrome, Firefox, IE, Safari). However, Opera only has half.

<img src="{{ site.url }}{{ site.baseurl }}/images/tree2.png">

After we control for browser, the test for “Opera” is significant. So, there is bug or bias for this level.

The plot below clearly indicates there is no “Opera” data in test group. There is no pint to keep “Opera” . Also, regards Chrome which has highest page visit number, however the average is almost the same as other browsers. Maybe, a lot people use chrome to visit page but just click once. In this way, safari behaviors better than other browsers.

<img src="{{ site.url }}{{ site.baseurl }}/images/opera.png">

We delete “Opera” from data and run the T-test again. Test group performs better than control group this time.

<img src="{{ site.url }}{{ site.baseurl }}/images/ttest2.png">

Novelty Effect:  
   First time users are obviously not affected by novelty effect. Look at test result btw new users in control group vs new users in test group.   
   If the test is winning overall, but not winning for the new users. It is a big sign of Novelty effect.   


* Conclusion & Suggestions    

   1) New feature improved engagement as expected in general. It seems we can keep the new feature for all users.    

   2) From browser aspect, it is important to check Chrome. Whether new feature looks the same as desired on Chrome. Maybe it is not looks good or the hyperlink of new future is
   defective, etc. In this aspect, Safari works great and people clicked more. However the data for browser is not complete, if we reply on this factor heavily, we need to recollect this part or debug the Opera issue.     

   3) Regards Novelty Effect, after control for new users, the (test/control-1 )ratio is a line close to 0, which may indicate Novelty Effect.   

   So, we’d like to keep the new feature for all users. But we have to pay more attention about novelty effect. More effort, no matter the design or recommendation content can be made in this point.
