---
layout: post
title: Using virtual environments on pip
image: /assets/img/blog/customer-seg/clustering-title-img.png
description: >
  In this project, we use k-means clustering to segment up our client's customer base in order to increase business understanding, and to enhance the relevancy of targeted messaging & customer communications.
tags: [KNN, Python, Clustering]
sitemap: true
hide_last_modified: true
---


https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/

to install virtual env, type this in Windows Command line:
pip3 install virtualenv
1. Navigate to your project folder
2. Create the virtual env:
`py -m venv env`
env is the name of the new environment, can be anything 
3. activate the environment 
`.\env\Scripts\activate`
4. checks:
- there should be a folder in ur project called env
- `cd env`
- `where python`
5. Install packages:
- using a requirements file
`pip install -r requirements.txt`
python is already installed, your requirements file should not contain python  - that gave me a lot of errors at first 
6. I got an error for the tensor flow install:
Could not find a version that satisfies the requirement tensorflow==2.3.0 . I upgraded pip using 
`pip install --upgrade pip` and then `pip install tensorflow`
That seemed to work out alright
6. To show all packages installed in your virtual env:
`pip list`
7. Another way is 
`pip freeze`
8. Create a reuirememts file 
`pip freeze > requirements.txt`
8. to leave the virtual environment
`deactivate`

To use an exisiting virtual envioronment, 
- cd to the folder where the virtual environment was created 
- activate the environment using 
`env_name\Scripts\activate`




  