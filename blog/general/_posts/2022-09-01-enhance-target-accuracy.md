---
layout: post
title: Enhancing Targeting Accuracy using ML
image: /assets/img/blog/enhance-target-accuracy/classification-title-img.png
description: >
  The goal for the project is to build a model that would accurately predict the customers that would sign up for our client's *delivery club* services. We use different classification algorithms to perform this task and understand what the main drivers are. 
sitemap: false
hide_last_modified: true
---

* toc
{:toc}


### Some Context

The goal for the project is to build a model that would accurately predict the customers that would sign up for our client's *delivery club* services.  This would allow for a much more targeted approach when running the next iteration of the delivery club campaign.  A secondary goal is to understand what the drivers for delivery club signups are, so the client can get closer to the customers that need or want this service, and enhance their messaging.

**Some context**: Our client, a grocery retailer, sent out mailers in a marketing campaign for their new *delivery club*.  This cost customers $100 per year for membership, and offered free grocery deliveries, rather than the normal cost of $10 per delivery. For this, they sent mailers to their entire customer base (apart from a control group) but this proved expensive.  **For the next batch of communications they would like to save costs by *only* mailing customers that were likely to sign up.**

Based upon the results of the last campaign and the customer data available, we will look to understand the *probability* of customers signing up for the *delivery club*.  This would allow the client to mail a more targeted selection of customers, lowering costs, and improving ROI.

We will use different classification algorithms to take on this task! 
<br>

**More details on the project can be found in the Jupyter Notebook here: [Enhancing Targeting Accuracy](https://github.com/ibiene-ds/enhancing-targeting-accuracy)**
<br>

### Results

The goal for the project was to build a model that would accurately predict the customers that would sign up for the *delivery club*.  This would allow for a much more targeted approach when running the next iteration of the campaign.  A secondary goal was to understand what the drivers for this are, so the client can get closer to the customers that need or want this service, and enhance their messaging.

Based upon these, the chosen model is the Random Forest as it was a) the most consistently performant on the test set across classication accuracy, precision, recall, and f1-score, and b) the feature importance and permutation importance allows the client an understanding of the key drivers behind *delivery club* signups. See table below for summary of all model results.
<br>
<br>
![alt text](/assets/img/blog/enhance-target-accuracy/model_summary.png)
<br> 
<br>   

- **Accuracy**: A very intuitive metric, the accuracy measures the number of correct classification predictions out of all predictions made. This number could be very misleading when you have very imbalanced data. An example of imbalanced data is a dataset where we have a 98%/2% split across 2 classes. 
- **Precision**: Answers the question: of all observations predicted as positive, what proportion was actually positive?
- **Recall**: Answers the question: of all positive observations, how many did we predict as positive?  <br>
Usually, trying to improve *Precision* has the opposite effect on *Recall* and vice-versa. So what metric to focus on is purely based on the project goals. 
- **F1-score**: Harmonic mean of Precision and Recall. A good F1-score comes when there is a balance between precision and recall. 

### Key Drivers of Delivery Club Signups

As well, the feature importances and permutation importances of the various input variables are shown below. This shows the key drivers behind the delivery club signups, which in this case are: Distance from store and Transaction Count.

![alt text](/assets/img/blog/enhance-target-accuracy/rf-classification-feature-importance.png)
<br>
<br>
![alt text](/assets/img/blog/enhance-target-accuracy/rf-classification-permutation-importance.png)



# Application <a name="modelling-application"></a>

We now have a model object, and the required pre-processing steps to use this model for the next *delivery club* campaign.  When this is ready to launch we can aggregate the neccessary customer information and pass it through, obtaining predicted probabilities for each customer signing up.

Based upon this, we can work with the client to discuss where their budget can stretch to, and contact only the customers with a high propensity to join.  This will drastically reduce marketing costs, and result in a much improved ROI.

___
<br>
# Growth & Next Steps <a name="growth-next-steps"></a>

While predictive accuracy was relatively high - other modelling approaches could be tested, especially those somewhat similar to Random Forest, for example XGBoost, LightGBM to see if even more accuracy could be gained.

We could even look to tune the hyperparameters of the Random Forest, notably regularisation parameters such as tree depth, as well as potentially training on a higher number of Decision Trees in the Random Forest.

From a data point of view, further variables could be collected, and further feature engineering could be undertaken to ensure that we have as much useful information available for predicting customer loyalty.
