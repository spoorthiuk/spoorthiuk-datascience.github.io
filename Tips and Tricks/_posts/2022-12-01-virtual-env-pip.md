---
layout: post
title: 10 steps to using Virtual Environments with pip
image: /assets/img/blog/virtual-env-cover.png
description: >
  Creating, Activating and De-activating virtual environments
tags: [venv, virtual environments, pip, python, pip3]
sitemap: true
hide_last_modified: true
---

Photo by <a href="https://unsplash.com/ja/@danique_dohmen?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Danique Dohmen</a> on <a href="https://unsplash.com/s/photos/neon-cubes?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
{:.figcaption}


Virtual environments were always the bane of my existence (since I use pip instead of conda). After a lot of research (erm...googling), I finally found a series of processes that worked for me - and I documented it to help others and remind myself. 

**Why do you need virtual environments?** <br>
For instance, say you are writing a program that needs various packages and their sometimes numerous dependencies. To make sure that you do not run into versioning issues, it might be cleaner to create a virtual environment where all the packages required to run the program or project are static and do not change. I had to do this when I started running Deep Learning projects since TensorFlow for instance would only work on specific versions of Python. 

I found the links below very useful in understanding virtual environments:

[Installing virtual environments using pip](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/) <br>
[Virtual Environments Tutorial](https://carpentries-incubator.github.io/python-intermediate-development/12-virtual-environments/index.html)

The following steps below are what I use to create virtual environments using pip. 

**Step 0: To create a virtual environment, type this in your Windows Command line**: <br>
`pip3 install virtualenv` <br>
Note that the command above will create the virtual environment with the Python version on your local computer. <br

To *install multiple versions of Python* on your computer, you need *pyenv*.  I found a really helpful [blog](https://k0nze.dev/posts/install-pyenv-venv-vscode/) and [video](https://www.youtube.com/watch?v=HTx18uyyHw8) by k0nze that gives a clear step-by-step of the entire process. 

1. Navigate to the project folder where you want the virtual environment to live using `cd` in the Command line.
2. Create the virtual environment:
`py -m venv env`
*env* is the name of the new environment and can be named anything — for example `py -m venv deeplearning`.
3. Activate the environment: `.\env\Scripts\activate`. Again, note that *env* is the name of the new environment. 
4. Do some basic checks:
- There should be a folder in your project folder called *env*
  - Go to the new environment: `cd env`
  - Check for Python install: `where python`
5. Install the required packages for your project using the following command: `pip install -r requirements.txt` <br> 
  Using a *requirements file* is the most efficient way of installing packages. See an example of a requirements file <link to picture>
 <br>
  Since Python is already installed, your requirements file should not contain Python  - that gave me a lot of errors at first. <br> I also got an error when pip tried to install TensorFlow (I was doing a Deep Learning project when I wrote this post). The error was: *Could not find a version that satisfies the requirement tensorflow==2.3.0* <br>
  To fix the error, I upgraded pip by running: `pip install --upgrade pip` and then `pip install tensorflow`. That seemed to fix things. Also, check the [TensorFlow official website](https://www.tensorflow.org/install/pip) to find what versions of Python are compatible with the latest release of TensorFlow. At this time, TensorFlow was not compatible with Python 3.11 (so I had to downgrade to 3.7). 
6. To show all packages installed in your virtual environment:
`pip list` or `pip freeze`
7. Create a requirements file 
`pip freeze > requirements.txt`
8. To leave the virtual environment:
`deactivate`
9. To use an existing virtual environment:
  - Navigate to the folder where the virtual environment was created in Windows terminal. <br>
  `cd path-to-directory` <br>
  - Activate the environment using `.\env_name\Scripts\activate`
10. You are now a virtual environment expert :) Well, at the very least, you are familiar with the basics as I am! 

Good luck!



  