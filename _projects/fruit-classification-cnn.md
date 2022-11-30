---
layout: project
title: Fruit Classification with Convolutional Neural Networks
caption: In this project, I build & optimize a Convolutional Neural Network to classify images of fruits to help a grocery retailer enhance & scale their sorting & delivery processes. 
description: >
  Classify fruits using a convolutional neural network
date: 19 Nov 2022
image: 
  path: /assets/img/blog/fruit-class-cnn/cnn-fruit-classification-title-img.png
sitemap: true
---

[![](https://img.shields.io/badge/Read_Full_Analysis-blue?)](/blog/fruit-classification-cnn/)
[![](https://img.shields.io/badge/Jupyter-Open_Notebook-blue?logo=Jupyter)](https://github.com/ibiene-ds/enhancing-targeting-accuracy/blob/main/Enhancing%20Target.ipynb)
[![](https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub)](https://github.com/ibiene-ds/fruit-classification-cnn)

In this project, I built a convolutional neural network (CNN) that classifies pictures of fruits with ~98% accuracy. A little bit of context here: at a recent tech conference, the grocery store managers spoke to a contact from a robotics company that creates robotic solutions that help other businesses scale and optimize their operations. Their representative mentioned that they had built a prototype for a robotic sorting arm that could be used to pick up and move products off a platform.  It would use a camera to "see" the product and could be programmed to move that particular product into a designated bin, for further processing. The only thing they hadn't figured out was how to *actually* identify each product using the camera so that the robotic arm could move it to the right place. We were asked to put forward a proof of concept on this - and were given some sample images of fruits from their processing platform. If this was successful and put into place on a larger scale, the client would be able to enhance their sorting & delivery processes.

The client provided some sample data which is made up of images of six different types of fruit, sitting on the landing platform in the warehouse. All images are of size 300 x 200 pixels. The data was randomly split the images for each fruit into training (60%), validation (30%) and test (10%) sets. For ease of use in Keras, our folder structure first splits into training, validation, and test directories, and within each of those is split again into directories based upon the six fruit classes.

The network was initialized with random variables (using the Sequential approach) and then accuracy was improved using Dropout, which operates like an ensemble decision tree model, and Image Augmentation which creates different aspects of the images (within reason) so the network can learn more generally and predict more accurately. Note that in building the network, we assumed a number of convolutional and dense layers and that gave us a pretty high accuracy score, but not to leave anything to chance, I also tuned the network using keras tuner to optimize the number of layers (both convolutional and dense), filters, type of optimizer and evaluate if we even need Dropout. The fully tuned model gave us a higher accuracy at 98.8%, which is comparable to using the VGG-16 model (popular model that won the IMAGENET competition). 

In the **Full Analysis**, I go through the details of creating the network; the **Jupyter Notebook**k contains the full code for creating the network used in the project. 


<br>
![alt text](/assets/img/blog/fruit-class-cnn/cnn-image-examples.png)

{:.figcaption}
Examples of Fruit Images in Data
<br>


