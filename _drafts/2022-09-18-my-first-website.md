---
layout: post
title: Building my Data Science Portfolio using Jekyll and Netlify
image: /assets/img/blog/pca-title-img.png
description: >
  How I built my Data Science Portfolio (from start to ongoing...)
tags: [Portfolio, Data Science, Jekyll, Netlify, Github]
sitemap: false
hide_last_modified: true
---

* toc
{:toc}


# How I started

So I got interested in Data Science and Machine Learning quite by accident - a conference! Well, most of my job as a reservoir engineer in the Oil and Gas Industry involves extracting insights from data - but I mostly used Excel and Tableau. At a conference however, my eyes got opened to the world of Machine Learning so I started to learn more. 

After going in a lot of rabbit holes on 'how to' advance my skillset, it all boiled down to a couple things: yes, do online courses but most importantly, keep doing projects and documenting them. Now I was good at the courses and starting projects but total rubbish at documenting my progress (mostly due to imposter syndrome and really, I didn't know how to start). 

A lot of Youtube videos and articles later (thank you @KenJee, @thedataprofessor, @dataslice), and a lot of learning on how not to do things (umm, failed attempts), I took the step and started building my portfolio website. 

This is intended to be a guide on how to build your portfolio/blog/website if you are just starting out and intimnidated by the thought of building a website (what?!!!) and showcasing your work. It is definitely not an exhaustive guide on the issues you may encounter, but my experiences and the resources and tools I found helpful along the way. 

Jekyll or Hugo appear to be two of the most popular static site generators in use. This blog deals only with Jekyll - I find it more beginner-friendly, but after watching a lot of videos on the subject, I daresay being handy with Jekyll means you can switch over to Hugo at any point.


# Step 0: Install Jekyll
Install Jekyll. Find instructions here (insert link). This step enables you to run your website on a local server. More on that later. 
Create  (add link) a Github account, or login if you have one already.

# Step 1: Find a theme and fork the repository (repo)
Find a Jekyll theme you like. Link to Resources here: jekyll-themes.io or .org
Or better still, do some sleuthing online (google data science portfolios) and find a portfolio you like, headover to their github and fork the repo! Chances are they have made a few tweaks to the files which means you don't have to re-invent the wheel.
You can rename the repo here as well. Let's call it *website*
(I am assuming you have a Github account and understand the basicsof git commands like cloning and forking). 
Click here (insert link)for a review of essential git commands.

# Step 2: Clone the Repo
Now you have the forked over repo in your Github (basically you have a copy of the repo in your Github account). 
Clone the repo (website) to your local computer. This copies the files to our local computer where we will edit the codes, and then later on, push to our Github account. 
To clone the repo, go to command line using Anaconda or CMD:
- Change directory to Desktop or anywhere else on your computer:
  cd Desktop or cd FolderName
- Go to Github and navigate to your forked repo (website). Open up the repo and go to the green CODE button at the top of the page and click. it will show an option to copy. Copy. 
- Back to CMD:
  git clone (location you copied). Use Ctrl+V

_Add some pictures of the green CODE button and git commands_

# Step 3: Jekyll Folder Structure
Open up VS Code or any UI you use (Atom, etc) and open up the folder (website) you cloned to your local computer. 
I typically use VS Code to edit and run code and notebooks (but feel free to use whatever you are comfortable with).  

_Things to note about Jekyll folder structure_
Jekyll themes are more or less similar in how they are structured. See example of the hydejack theme file structure I used in the picture below (add picture):
 -*_config.yml_: Your website's general settings. Changing this file usually means you hit Ctrl+C to stop the local server and regenerate your website. No big deal. 
 -*_site_ folder: Generates the files for your website. Do not touch. 
 -*assets*: Usually contains stuff like images and icons for your website. 

 I found this post that really goes into the details. Very informative. (google jekyll vs hugo)

 Open terminal (Ctrl + '), and run this: 

 *bundle exec jekyll serve*

 This opens up a local hosting site where you can see your changes as you make them to the various files. Copy the server site address generated to your web browser and a local version of your site will appear. Voila! Now when you make changes to any of the files in the folder (website), it'll appear on the site. However, if you make a change to the _config.yml file, you'll have to stop running the server (Ctrl+C) in Terminal and re-run the command *bundle exec jekyll serve* again.


# Step 4: Edit the _config.yml file
Edit the _config.yml file. It's usually quite self explanatory - the creators give lots of guidance - so do well to read the comments. Replace the fillers with your own name, email address, socials etc. See example picture below:

Ctrl + C to stop running the server.

Then run *bundle exec jekyll serve* to restart the server to see your changes.

# Step 5: Your first post/contents of your portfolio
There is usually a _posts folder in the hierarchy - you can edit that and start putting content in. There is usually a template given for the names of the posts, make sure to follow that.

Useful links for writing in markdown (I found inline images quite finicky but finally got the hang of it):
Link 1
Link 2
Link 3

If you are confused on how to structure content or what projects to add in your portfolio, take a look at some of these amazing portfolios and you'll soon get an idea. See links below:
Link 1
Link 2
Link 3

Word of advice though: Every savant was once an amateur (in other words, do not despise the days of small beginnings). Do not shy away from putting what you consider "small" projects on: As you progress in your jounrey, you can add and subtract from your portfolio - the key is to keep doing projects. The more you do, the better you'll become and the more confident you'll feel - just keep moving. 

# Optional pretty stuff:
## Shields:
So I spent the better part of an hour trying to figure out how to add cool buttons that would link to my Github account or a Jupyter notebook (saw the idea in other people's portfolios and I thought it was an awesome way of laying stuff out). All of that googling and research on stackoverflow led me to the wonder of *shields* (Go to shields.io to learn more, add link). I have to give a shout to Chris Tran here (link to Chris Tran) - reading his blog really helped me with this idea:

Basically, you can create shields using this format:

*https://img.shields.io.badge/<AppName>-<Message>-<htmlcolorcode>?logo=<AppName>*

Example: https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub

More formatting options available on shields.io

To create links to another site (like Github or a Jupyter Notebook), use the format below:

[![](https://img.shields.io/badge/Read_Full_Analysis-blue?)](/blog/enhance-target-accuracy/)
[![](https://img.shields.io/badge/Jupyter-Open_Notebook-blue?logo=Jupyter)](/project-files/enhance-target-accuracy-ml.html)
[![](https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub)](https://github.com/ibiene-ds/enhancing-targeting-accuracy)

The code above gives you these pretty buttons/shields

Add picture:

I found those extremely useful - now I could give a very concise summary of a project, and link interested readers to either the full analysis or the Jupyter notebook or the Web App - in essence, readers can chose the level of detail they want. 

## Exporting Jupyter Notebooks to .html files:
Install using pip
To export a notebook, 
- cd to the folder of interest 
- 

# Step 6: Push to Github
You have created some posts, you love your blog and hopefully, you've added a personal profile about yourself and some snazzy shots. Let's push this to our Github repo using:

git push origin main 
or 
git push origin master 
or 
git push


# Step 6: Deploy online
So far, no one can access your website because it is on your local computer - but what's the point of a blog if only you can read it? So time to deploy.

You can either use Github or Netlify to host your website for free. 

## Github: 
If you have only one site on your account- it is pretty straightforward. Go to your repo (website) settings, and change your repo name to <githubusername>.github.io. 

For example, my github user name is ibiene-ds so my repo name would be *ibiene-ds.github.io*. This tells Github that this is a website (I'm sure there are more technicalities to that but that is it in a nut shell). Give it a minute or two, and you'll get a message like this:

[Add a picture]

Your site is live! Go over to that site and take a look your website.

If you have more than one site on your Github account, there are a couple more steps:
- Name your repo, say website
- Go to Settings and navigate to Github Pages
- next steps....


## Netlify: 
*Diclosure - I started hosting on Github and then it became finicky with a second site, still don't completely understand it - some sites worked, and some didn't, so moved to Netflify and wow - so easy!*

Go to netlify.com to create an account. Follow the steps to connect your Github account. I found this tutorial on their site really straightforward and useful. [Insert Link here]

Your site is now deployed at a subdomain (netlify.app or netlify.com)

You can go ahead and change your site name (recommended), or use a custom domain (optional)

# Step 7: Index your site 
Now you have a portfolio website showing your projects. But I quickly learned that deploying a website on Github or Netlify does not necessarily mean that search engines like Google or Bing will automatically find it (try it!). So I got googling again and found these resources to help with that issue.

Link 1
Link 2 
Link 3 

I will condense the steps I took here:





And you are done! You have a portfolio website - now just keep doing projects and adding to it!














