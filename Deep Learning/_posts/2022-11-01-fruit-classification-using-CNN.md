---
layout: post
title: Fruit Classification using CNN
image: 
  path: /assets/img/blog/fruit-class-cnn/cnn-fruit-classification-title-img.png
  width: 800
  height: 600
description: >
  The goal for the project is to build a convolutional neural network (CNN) that would classify fruits for a robotics company, for use in sorting grocery items. We use Image Augmentation and Dropout to enhance the performance of the netwrk and used keras tuner to come up with the optimal setup for the highest accuracy. 
tags: [Computer Vision, Python, Deep Learning, Neural Networks, CNN]
sitemap: true
hide_last_modified: true
---

[![](https://img.shields.io/badge/Jupyter-Open_Notebook-blue?logo=Jupyter)](https://github.com/ibiene-ds/enhancing-targeting-accuracy/blob/main/Enhancing%20Targeting%20Accuracy%20using%20ML.ipynb)
[![](https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub)](https://github.com/ibiene-ds/enhancing-targeting-accuracy)

* toc
{:toc}

## Project Overview and Results

**Problem Statement**: Our client, a grocery retailer, sent out mailers in a marketing campaign for their new *delivery club*.  This cost customers $100 per year for membership, and offered free grocery deliveries, rather than the normal cost of $10 per delivery. For this, they sent mailers to their entire customer base (apart from a control group) but this proved expensive.  **For the next batch of communications, they would like to save costs by *only* mailing customers that were likely to sign up.** Based on the results of the last campaign and the customer data available, we will look to understand the *probability* of customers signing up for the *delivery club*.  This would allow the client to mail a more targeted selection of customers, lowering costs, and improving ROI.

The goal of this project is to build a model that would accurately predict the customers that would sign up for our client's *delivery club* services.  This would allow for a much more targeted approach when running the next iteration of the delivery club campaign.  A secondary goal is to understand what the drivers for delivery club signups are, so the client can get closer to the customers that need or want this service, and enhance their messaging.

The data was cleaned, preprocessed and split into training and testing sets; four different models were used in the modelling process and based on the goals of the project, the model of choice is the **Random Forest** model as it was:
- the most consistent performant on the test set across classification accuracy, precision, recall, and F1-score, and  
- the feature importance and permutation importance allow the client an understanding of the key drivers behind *delivery club* signups. See the table below for a summary of all model results.
<br>
<br>
![alt text](/assets/img/blog/enhance-target-accuracy/model_summary.png)



## Data Overview
We will be predicting the binary *signup flag* from the *campaign_data* table in the client database. The key variables to predict this will come from different tables, which we have joined and aggregated to come up with the final dataset. We focused on aggregating data 3 months before the last campaign date. 

The final table of data for modelling looks something like this:

| **Variable Name** | **Variable Type** | **Description** |
|---|---|---|
| signup_flag | Dependent | A binary variable showing if the customer signed up for the delivery club in the last campaign |
| distance_from_store | Independent | The distance in miles from the customers home address, and the store |
| gender | Independent | The gender provided by the customer |
| credit_score | Independent | The customers most recent credit score |
| total_sales | Independent | Total spend by the customer in ABC Grocery - 3 months pre campaign |
| total_items | Independent | Total products purchased by the customer in ABC Grocery - 3 months pre campaign |
| transaction_count | Independent | Total unique transactions made by the customer in ABC Grocery - 3 months pre campaign |
| product_area_count | Independent | The number of product areas within ABC Grocery the customers has shopped into - 3 months pre campaign |
| average_basket_value | Independent | The average spend per transaction for the customer in ABC Grocery - 3 months pre campaign |
{:.smaller}

## Data Pipeline

Before we get to building the network architecture, & subsequently training & testing it - we need to set up a pipeline for our images to flow through, from our local hard-drive where they are located, to, and through our network.

In the code below, we:

* Import the required packages
* Set up the parameters for our pipeline
* Set up our image generators to process the images as they come in
* Set up our generator flow - specifying what we want to pass in for each iteration of training

```python

# import required packages
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Conv2D, MaxPooling2D, Activation, Flatten, Dense, Dropout
from tensorflow.keras.preprocessing.image import ImageDataGenerator
from tensorflow.keras.callbacks import ModelCheckpoint
from keras_tuner.tuners import RandomSearch
from keras_tuner.engine.hyperparameters import HyperParameters
import os

# data flow parameters

training_data_dir = '/Deep Learning/CNN/data/training'
validation_data_dir = '/Deep Learning/CNN/data/validation'
batch_size = 32
img_width = 128
img_height = 128
num_channels = 3
num_classes = 6

```
In the code above, we have specified that the images will be processed in batches of 32; we have also standardized the pixel size of all the images to a standard 128 x 128 (it can be any size we choose but it is easier for the network if we have a standard size for all pictures). We have also parametrized the number of classes. 


Next. we simply use the generators to rescale the raw pixel values (ranging between 0 and 255) to float values that exist between 0 and 1.  The reason we do this is mainly to help Gradient Descent find an optimal, or near optional solution each time much more efficiently - in other words, it means that the features that are learned in the depths of the network are of a similar magnitude, and the learning rate that is applied to descend down the loss or cost function across many dimensions, is somewhat proportionally similar across all dimensions - and long story short, means training time is faster as Gradient Descent can converge faster each time!

We also apply image augmentation to cause the network to learn from different angles and zoom sizes a picture may come in. The augmentation parameters are just educated guesses for now but we'll see how they contribute to the accuracy of the model. Note that augmentation is only done on the training data, never on validation or test data. 

```python 
training_generator = ImageDataGenerator(rescale = 1./255, 
                                       rotation_range = 20, 
                                       width_shift_range = 0.2, 
                                       height_shift_range = 0.2, 
                                       zoom_range = 0.1, 
                                       horizontal_flip = True, 
                                       brightness_range = (0.5, 1.5), 
                                       fill_mode = 'nearest')

validation_generator = ImageDataGenerator(rescale = 1./255)

# image flows
training_set = training_generator.flow_from_directory(directory = training_data_dir, 
                                                      target_size = (img_width, img_height), 
                                                      batch_size = batch_size, 
                                                      class_mode = 'categorical')

validation_set = validation_generator.flow_from_directory(directory = validation_data_dir, 
                                                          target_size = (img_width, img_height), 
                                                          batch_size = batch_size, 
                                                          class_mode = 'categorical')

```



With this pipeline in place, our images will be extracted, in batches of 32, from our hard-drive, where they're being stored and sent into our model for training. 

## Network Architecture

Our baseline network is simple, but gives us a starting point to refine from.  This network contains **2 Convolutional Layers**, each with **32 filters** and subsequent **Max Pooling** Layers.  We have a **single Dense (Fully Connected) layer** following flattening with **32 neurons** followed by our output layer.  We apply the **relu** activation function on all layers, and use the **adam** optimizer.


