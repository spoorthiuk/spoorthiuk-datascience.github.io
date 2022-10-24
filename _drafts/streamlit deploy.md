---
layout: post
title: Deploying a web app on Streamlit
image: /assets/img/blog/customer-seg/clustering-title-img.png
description: >
  In this project, we use k-means clustering to segment up our client's customer base in order to increase business understanding, and to enhance the relevancy of targeted messaging & customer communications.
tags: [KNN, Python, Clustering]
sitemap: true
hide_last_modified: true
---

1. Create a folder that would house all your document. The final contents of the folder would be:
  - app.py
  - requirements.txt 

2. The app.py file
This file contains the python script to be executed. 

3. The requirements.txt file 
This is needed so that Streamlit knows what version of packages you used in your app. To know what version of, say, pandas you have installed, open command line and run: `pip show pandas`
(show pic of requirements file)

4. in command line, type: `streamlit run app.py`. This creates a local web server so you can see your changes/edits live as you edit your script (app.py)

5. Once you are satisfied, push to your git repo. See [instructions](blog) here:

6. Host the app online. Go to share.streamlit.io, connect to the repo and add the new app. Streamlit does the rest!

https://ibiene-ds-weight-tracker-app-app-jc89ye.streamlitapp.com/

