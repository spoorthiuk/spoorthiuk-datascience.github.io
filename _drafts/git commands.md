---
layout: post
title: Popular Git Commands
image: /assets/img/blog/customer-seg/clustering-title-img.png
description: >
  In this project, we use k-means clustering to segment up our client's customer base in order to increase business understanding, and to enhance the relevancy of targeted messaging & customer communications.
tags: [KNN, Python, Clustering]
sitemap: true
hide_last_modified: true
---

* toc
{:toc}

Let's start with the technicalities: Git is a version control system used for tracking modifications in source code in software development while GitHub is a collaboration and version control platform for storing and managing code. More on the differences [here](https://www.simplilearn.com/tutorials/git-tutorial/git-vs-github). GitHub is a version control tool used by programmers worldwide; other variations of this service are GitLab, Bitbucket etc. This is very useful in showcasing your work (you can save your scripts and your Jupyter notebooks here), you can also host your website here. 

This is by no means an exhaustive list of commands but what I use regularly. The steps below used to live on a text file on my local computer which I consulted from time to time. Hope it serves you well!

## Downloading Git for Windows
To download Git, go to [https://git-scm.com/download/win](https://git-scm.com/download/win) and follow the prompts.

## Pushing from a Local Repository to GitHub

1. On your local desktop or folder of interest, create a folder you want to clone into (ex: Palindrome function folder) 
and copy the address of the folder
2. Open up Command Line and navigate to the folder using:
 `cd C:\Users\Ibiene\OneDrive\DataScience_MachineLearning\my new folder`
3. Next, initialize git:
  `git init`
4. To add all files to your local git reposiory:
  `git add .`
5. Next, commit:
  `git commit -m "first commit"`
6. On GitHub, create a new repo, name repo but do not add a readme file 
	- copy code that comes up
7. Back to command line, run the command below to connect your local folder to the remote git repositoey:
  `git remote add origin https://github.com/ibiene-ds/palindrome-function.git`
8. To verify that you have a successful connection, 
  `git remote -v`
If an error comes up: remote origin already exists, type this:
  - Remove remote repo:
    `git remote rm origin`
  - Repeat steps 7 and 8
9.  Push the contents of your local repo to remote repo:
  `git push -u origin main` OR 
  `git push origin master` (if main does not work)git stat
10. To check status:
   `git status`

## Pushing from a remote repo to local folder

OR start from here (cloning repo on github to local and making changes)
navigate to ur working folder using cd ...
1. Create new repo on GitHub, name the repo and add a README file
1. Go to existing repo
2. Using the green button called code - copy the location of the repo 
3. In command line, clone the repo into your local computer:
	`git clone https://github.com/ibiene-ds/myrepo.git`
Check your current folder on file explorer to make sure the command is successful.
4. In command line, go to your cloned repo:
  `cd path/to/new/folder`
Now you can make changes to files on your local computer, save and then push to GitHub when you are satisfied.

Other useful git commands:
- `git status` -  to show changes between local and cloud repo
- `git add.` - add all files in a folder, ready to commit 
- `git commit -a -m  "added x"`
  - *-a* means all changes that were made, 
  - *-m* means commit message, implies you will add a commit message like "changed image dimensions"
- `git push -u origin main` or `git push` (works well too)

Make changes in GitHub and pull into local repo:
- `git fetch origin` 
- `git status`
- `git pull origin main`


