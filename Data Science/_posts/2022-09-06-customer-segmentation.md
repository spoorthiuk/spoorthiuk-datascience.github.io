---
layout: post
title: The "You Are What You Eat" Customer Segmentation
image: /assets/img/blog/customer-seg/clustering-title-img.png {:width="800" height="600"}
description: >
  In this project, we use k-means clustering to segment up our client's customer base in order to increase business understanding, and to enhance the relevancy of targeted messaging & customer communications.
tags: [KNN, Python, Clustering]
sitemap: true
hide_last_modified: true
---

In this project, we use k-means clustering to segment up our client's customer base in order to increase business understanding, and to enhance the relevancy of targeted messaging & customer communications.

___

The Senior Management team from our client, a supermarket chain, are disagreeing about how customers are shopping, and how lifestyle choices may affect which food areas customers are shopping into, or more interestingly, not shopping into.

They have asked us to use their customer data and Machine Learning to help segment up their customers based upon their engagement with each of the major food categories - aiding business understanding of the customer base, and to enhance the relevancy of targeted messaging & customer communications.

Since this is an *unsupervised* classification problem, the k-Means clustering algorithm would do a superb job in segmenting the customer base. 
<br>
<br>
**More details on the project can be found in the Jupyter Notebook here: [Customer Segmentation](https://github.com/ibiene-ds/customer-segmentation)**
<br>
<br>

### Results

Based upon iterative testing using WCSS we settled on a customer segmentation with 3 clusters. These clusters ranged in size: <br>

- Cluster 0 accounted for 73.6% of the customer base, 
- Cluster 2 accounted for 14.6%, and 
- Cluster 1 accounted for 11.8%.

There were some extremely interesting findings from profiling the clusters.

For *Cluster 0*, we saw a significant portion of spend being allocated to each of the product areas - showing customers without any particular dietary preference.  

For *Cluster 1*, we saw quite high proportions of spend being allocated to Fruit & Vegetables, but very little to the Dairy & Meat product areas.  It could be hypothesised that these customers are following a vegan diet.  

Finally customers in *Cluster 2* spent significant portions within Dairy, Fruit & Vegetables, but very little in the Meat product area - so similarly, we would make an early hypothesis that these customers are more along the lines of those following a vegetarian diet.
<br>
<br>

### Growth/Next Steps

It would be interesting to run this clustering/segmentation at a lower level of product areas, so rather than just the four areas of Meat, Dairy, Fruit, Vegetables - clustering spend across the sub-categories *below* those categories.  This would mean we could create more specific clusters, and get an even more granular understanding of dietary preferences within the customer base.

Here we've just focused on variables that are linked directly to sales - it could be interesting to also include customer metrics such as distance to store, gender etc to give a even more well-rounded customer segmentation.

It would be useful to test other clustering approaches such as hierarchical clustering or DBSCAN to compare the results.
<br>
<br>

___
