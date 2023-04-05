---
layout: post
title: Popular Git Commands
image: /assets/img/blog/github-images/git-cover-image.jpg
description: >
  This blog briefly goes through some essential git commands that may prove handy.
tags: [Git, GitHub, Version Control, Code]
sitemap: true
hide_last_modified: true
---

* toc
{:toc}

Let's start with the technicalities: Git is a version control system that tracks source code modifications in software development, while GitHub is a collaboration and version control platform for storing and managing code. More on the differences [here](https://www.simplilearn.com/tutorials/git-tutorial/git-vs-github). GitHub is a version control tool used by programmers worldwide; other variations of this service are GitLab, Bitbucket, among others.

For the budding data scientist, GitHub can also be beneficial in showcasing your projects (scripts and notebooks) and used to host your portfolio website.

The following is not an exhaustive list of Git commands, but rather what I use regularly. The steps below lived on a text file on my local computer that I consulted often when I first started using Git. 

## Downloading Git for Windows
To download Git, go to the [__official git site__](https://git-scm.com/download/win) and follow the prompts. Select the defaults except you know better. 

## Pushing from a Local Repository to GitHub

* On your local desktop or folder of interest, create a new folder for your project and copy the address of the folder.
* Open up Command Line and navigate to the folder using: <br>
 `cd C:\Users\Ibiene\OneDrive\blog-test`
* Initialize git: <br>
  `git init`

  <br>

![](/assets/img/blog/github-images/git-init.png)

* On GitHub, create a new repository, name the repository but **DO NOT** add a readme file. 
* Copy the address of the repository. This address will be pasted in the next step.

![](/assets/img/blog/github-images/no-readme.png)
<br>

* Back to Command Line, run the command below to connect your local folder to the remote git repository: <br>
  `git remote add origin https://github.com/ibiene-ds/blog-test.git` <br> 
  Replace the example .git link with Ctrl+V - to paste the repository address you copied in the previous step.

* To verify that you have a successful connection: <br>
  `git remote -v`

![](/assets/img/blog/github-images/git-remote-v.png)

* If an error comes up such as *remote origin already exists*, try the following steps in Command Line:
    * Remove remote repo: <br>
      `git remote rm origin` <br>
    * Repeat `remote add...` & `git remote -v` commands. <br>

Usually, I get an error when I mistakenly add a README file at the beginning (when I created the repo). So my quick fix is deleting and re-creating the repository without the README file. 

## Adding, Committing and Pushing Files 

* To add all files to your local git repository: <br>
  `git add .` <br>
  The '.' means All. Alternatively, you can use: <br>
  `git add -A` <br>
  To add a single file, use: <br>
  `git add <file-name>`

* Next, commit:
  `git commit -m "added image dimensions"` <br>
  "-m" means message and implies that you will add a commit message such as "added image dimensions". <br>
  For your message, add a helpful comment about the changes you made so you can track the changes if you need to go back to a previous version. 

* Push the contents of your local repository to the remote repository: <br>
  `git push -u origin main` OR <br>
  `git push origin master`
  - The choice of **main** or **master** depends on your initial choices when you first installed git, but they both refer to your main *branch*. 
  - The message after your first commit should tell you what your main branch is called. For instance, mine is called 'master' so pushing to 'main' will generate errors.

  ![](/assets/img/blog/github-images/master-png.png)

* To check status:
   `git status`
 

## Pushing from a Remote Repository to a Local Folder

* Create a new repository on GitHub, name the repository and add a README file. 
* Enter into the new repository.
* Using the green button called **Code** - copy the location of the repo

![](/assets/img/blog/github-images/github-to-local-code.png) 

![](/assets/img/blog/github-images/github-to-local-code-button.png)

* In Command Line, navigate to your working folder and clone the repo into your local computer using the command: <br>
	`git clone https://github.com/ibiene-ds/myrepo.git`
  
* Go to your cloned repo: <br>
  `cd path/to/new/folder` 
  
Now, you can change files on your local computer, save and then push them to GitHub when satisfied.




