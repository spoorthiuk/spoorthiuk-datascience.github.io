---
layout: project
title: Fruit Classification with Convolutional Neural Networks
caption: In this project, I build & optimize a Convolutional Neural Network to classify images of fruits to help a grocery retailer enhance & scale their sorting & delivery processes. 
description: >
  Classify fruits using a Convolutional Neural Network
date: 19 Nov 2022
image: 
  path: /assets/img/blog/fruit-class-cnn/cnn-fruit-classification-title-img.png
sitemap: true
---

[![](https://img.shields.io/badge/Read_Full_Analysis-blue?)](/blog/fruit-classification-cnn/)
[![](https://img.shields.io/badge/Jupyter-Open_Notebook-blue?logo=Jupyter)](https://github.com/ibiene-ds/enhancing-targeting-accuracy/blob/main/Enhancing%20Target.ipynb)
[![](https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub)](https://github.com/ibiene-ds/fruit-classification-cnn)

In this project, I built a *Convolutional Neural Network (CNN)* that classifies pictures of fruits with **~98% accuracy**. 

## Problem Statement
At a recent tech conference, the grocery store managers spoke to a contact from a robotics company that creates robotic solutions that help other businesses scale and optimize their operations. Their representative mentioned that they had built a prototype for a robotic sorting arm that could be used to pick up and move products off a platform.  It would use a camera to "see" the product and could be programmed to move that particular product into a designated bin, for further processing. **The only thing they had not figured out was how to identify each product using the camera so that the robotic arm could move it to the right place. We were asked to put forward a proof of concept on this - and were given some sample images of fruits from their processing platform. **If this was successful and put into place on a larger scale, the client would be able to enhance their sorting & delivery processes.**

The client provided some sample data which is made up of images of six different types of fruits sitting on the landing platform in the warehouse. All images are of size 300 x 200 pixels. The images for each fruit were randomly split into Training (60%), Validation (30%) and Test (10%) sets. For ease of use in *Keras*, our folder structure first splits into training, validation, and test directories, and within each of those is split again into directories based upon the six fruit classes.

## Actions
We started by creating our pipeline for feeding training & validation images in batches - from our local directory into the network.  We investigated & quantified predictive performance epoch by epoch on the validation set, and then also on a held-back test set.

Our baseline network is simple but gave a good starting point to refine from.  This base network is made up of:  **2 Convolutional Layers**, each with **32 filters** and subsequent **Max Pooling** Layers.  We have a **single Dense (Fully Connected) layer** following flattening with **32 neurons** followed by our output layer.  We applied the **relu** activation function on all layers and use the **adam** optimizer.

For our first refinement, we added *Dropout* to tackle the issue of overfitting which is prevalent in the baseline network performance.  We use a *dropout rate of 0.5* which gave some good results and got rid of our overfitting problem. 

We then added  *Image Augmentation* to our data pipeline to increase the variation of input images for the network to learn from, resulting in more robust results as well as also address overfitting.

Note that in building the base network, we assumed several parameters such as the number of convolutional and dense layers and that gave us a pretty high accuracy score, but not to leave anything to chance, we also tuned the network using *keras-tuner* to optimize the hyperparameters such as the number of layers (both convolutional and dense), filters, type of optimizer among others. The best network is made of **3 Convolutional Layers**, each followed by **Max Pooling** Layers.  The first Convolutional Layer has **96 filters**, the second & third have **64 filters**.  The output of this third layer is flattened and passed to a **single Dense (Fully Connected) layer** with **160 neurons**.  The Dense Layer has **Dropout** applied with a **dropout rate of 0.5**.  The output from this is passed to the output layer.  Again, I used the **relu** activation function on all layers and use the **adam** optimizer.

Finally, we tested the pre-trained **VGG16** network on our dataset using **Transfer Learning**. This was done to compare our network's results against that of a pre-trained network. 

## Results
In terms of Classification Accuracy on the Test Set, we saw:
* Baseline Network: **80%**
* Baseline + Dropout: **85%**
* Baseline + Image Augmentation: **93%**
* Optimized Architecture + Dropout + Image Augmentation: **98%**
* Transfer Learning Using VGG16: **98%**

Tuning the network's architecture with Keras-Tuner gave us a great boost, but was also very time intensive - however, if this time investment results in improved accuracy then it is time well spent.

The use of Transfer Learning with the VGG16 architecture was also a great success, in only 10 epochs we were able to beat the performance of our smaller, custom networks which were training over 50 epochs.  From a business point of view, we also need to consider the overheads of (a) storing the much larger VGG16 network file and (b) any increased latency on inference.

In the **Full Analysis**, I go through all the details of creating the network; the **Jupyter Notebook** contains the full code for creating the network used in the project. 


<br>
![alt text](/assets/img/blog/fruit-class-cnn/cnn-image-examples.png)

{:.figcaption}
Examples of Fruit Images in Data
<br>


