---
layout: project
title: Enhancing target accuracy with Machine Learning
caption: Predict which customers will sign up for *Delivery Club*
description: >
  Use different classification models to predict what customers are likely to sign up for Delivery Club.
date: 1 Sept 2022
image: 
  path: /assets/img/projects/enhance-target-pic.jpg
sitemap: false
---

[![](https://img.shields.io/badge/Read_Full_Analysis-blue?)](/blog/enhance-target-accuracy/) &nbsp;
[![](https://img.shields.io/badge/Jupyter-Open_Notebook-blue?logo=Jupyter)](/project-files/enhance-target-accuracy-ml.html) &nbsp;
[![](https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub)](https://github.com/ibiene-ds/enhancing-targeting-accuracy)

In this project, I built a model that **predicts customers' likelihood to sign up for a grocery chain's delivery club initiative**. The end goal of the project is to **generate a list of customers (for the grocery chain) that are most likely to be receptive to mail advertisements the grocery chain will send to promote their *delivery club* initiative**. This will save the company some costs as marketing efforts would be targeted to where they would have the most impact. 

The dataset was mostly clean and missing values were excluded since they constitute less than 1% of the data.  Four classification models were used to generate predictions - *Logistic Regression, K Nearest Neighbors (KNN), Decision Tree and Random Forest*. Of all four models, the **Random Forest model gave the best F1-score (0.92) with an accuracy of 95.7%**. Feature and permutation importance plots show that **"distance from store"** is the primary driver for delivery club signups - thatis, the farther people are from the store, the more likely they are to sign up for a delivery club solution to save them the travel.

