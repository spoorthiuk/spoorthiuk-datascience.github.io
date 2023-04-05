---
layout: post
title: Building my Data Science Portfolio using Jekyll and Netlify
image: 
  path: /assets/img/blog/my-first-blog-cover.jpeg
  width: 800
  height: 600
description: >
  How I built my Data Science Portfolio (from start to ongoing...)
tags: [Portfolio, Data Science, Jekyll, Netlify, Github]
sitemap: true
hide_last_modified: true
---

* toc
{:toc}


## How I started

I got interested in Data Science and Machine Learning quite by accident. About 90% of my job as a Reservoir Engineer in the Oil and Gas Industry involves extracting insights from data - but I mostly used Excel and Tableau. At a conference, however, my eyes got opened to the world of Machine Learning so I started to learn more. 

After going in a lot of rabbit holes on how to advance my skill set, it all boiled down to a couple of things: yes, do online courses but most importantly, keep doing projects and documenting them. Now I was good at signing up for courses and starting projects but total rubbish at documenting my progress (mostly due to imposter syndrome and well, I didn't know how to start building a portfolio website). 

A lot of Youtube videos and articles later (thank you @KenJee, @thedataprofessor, @dataslice), and after a lot of learning on how not to do things (umm, failed attempts), I took the step and started building my portfolio website. 

This blog is intended to be a guide on how to build your portfolio/blog/website if you are just starting and intimidated by the thought of building a website (what?!!!) and showcasing your work. It is not an exhaustive guide on the issues you may encounter in the process, but rather my experiences and the resources and tools I found helpful along the way. 

First, you are likely going to use a static site generator. Jekyll or Hugo appears to be two of the most popular static site generators in use. This blog deals only with Jekyll - I find it more beginner-friendly, but after watching a lot of videos on the subject and building my website, I daresay being handy with Jekyll means you can switch over to Hugo at any point. Let's get started.


## Step 0: Install Jekyll & Create GitHub Account
- Find instructions to install Jekyll [here](https://jekyllrb.com/docs/installation/windows/). I used the first option: **Installation via RubyInstaller**. This step enables you to run your website on a local server. More on that later. I ran into a lot of dependency issues using the most recent version of Ruby+Devkit, so after doing a lot of research, I installed the *v2.7.6.*

**Update: I recently bought a new laptop and had to re-install Ruby. I used the instructions above but could not find v2.7.6, so I ended up using this version (v3.1.3) as recommended by the program creators.**

- [Create](https://github.com/) a GitHub account, or log in if you have one already.

## Step 1: Find a theme and fork the repository (repo)
Find a Jekyll theme you like. You can find a vast array of Jekyll themes in the resources below: 
- [GitHub.com Jekyll Themes](https://github.com/topics/jekyll-theme)
- [jamstackthemes.dev](jamstackthemes.dev)
- [jekyllthemes.org](jekyllthemes.org)
- [jekyllthemes.io](jekyllthemes.io)
- [jekyll-themes.com](jekyll-themes.com) <br>

Check out the **demos** available on the sites  - and once you decide on a theme, either the *Download* or *Go to GitHub* button will take you to GitHub so you can *fork* the repository. 

Or better still, do some sleuthing online (literally google *data science portfolios*) and find a portfolio you like, head over to the author's GitHub account and fork the repo! Chances are they have made a few tweaks to the base files which means you do not have to re-invent the wheel.
Let's call the forked-over repo **website**. <br>

I am assuming you have a GitHub account and understand the basics of **git commands** like *cloning* and *forking*. Click [here](https://towardsdatascience.com/essential-git-commands-every-programmer-should-know-fe96feb570ce) for a review of essential git commands.

## Step 2: Clone the Repository
Now you have the *forked* repo in your GitHub (which means you have a copy of the repo in your GitHub account).
*Clone* the repo (**website**) to your local computer. This copies the files to your local computer where you will edit the codes, and then, later on, push them to your GitHub account. <br>  

To clone the repo, go to command line (*type CMD in Windows search bar*) and complete the following steps:
- Change directory to Desktop or anywhere else you prefer on your computer.  
  - `cd Desktop` or `cd YourFolderName`
- Go to GitHub and navigate to your forked repo (**website**). Open up the repo and click the green **Code** button near the top of the page. Copy. <br>
- Back to command line (*tip - Use Ctrl+V to paste the remote address you copied*)
  - `git clone https://github.com/ibiene-ds/website.git`

<br> 

![alt text](/assets/img/blog/code-button-github.png)


## Step 3: Jekyll Folder Structure/Local Server
- Open up Visual Studio Code or any code editor you use (ex: Atom) and navigate to the folder (**website**) you cloned to your local computer. I typically use VS Code to edit and run code but feel free to use whatever you are comfortable with.  

  **Things to note about Jekyll folder structure** <br>

  Jekyll themes are similar in how they are structured. See the example of the [Hydejack](hydejack.com) theme file structure I used in the official GitHub [repo](https://github.com/hydecorp/hydejack).

  Some important files to note:

  - *_config.yml*: Your website's general settings. Changing this file usually means you hit Ctrl+C to stop the local server and regenerate your website. No big deal. 
  - *_site folder: Generates the files for your website. **Do not touch.
  - *_assets folder: Usually contain stuff like images and icons for your website. 

  I found this very informative [post](https://www.freecodecamp.org/news/hugo-vs-jekyll-battle-of-static-site-generator-themes/) that goes into the details.

  Another good resource that helped me understand the Jekyll file structure is the [YouTube video](https://www.youtube.com/watch?v=wCOInE7-E0I), which is Part 1 of a series by Dataslice.

- In Visual Studio, open terminal (Ctrl + `) and run this command: 

  `bundle exec jekyll serve`

  This opens up a **local hosting site** where you can see changes as you make them to the various files. **Copy the server site address** generated to your web browser and a local version of your site will appear. Voila! Now when you make changes to any of the files in the folder (**website**), it would reflect on the website. <br>  
  Note that **if you make a change to the _config.yml file**, you would need to **stop** running the server **(Ctrl+C)** in VS Code terminal and re-run the command `bundle exec jekyll serve`.

  If you get an error, run `bundle install` - that command should install a bunch of stuff to fix things. Once it's done, run `bundle exec jekyll serve` again. 


## Step 4: General website configuration and customization
- **Edit the _config.yml file**. It is usually quite self-explanatory as the theme creators often give a lot of guidance - so do well to read the **theme documentation**. Replace the fillers with your name, email address, socials etc. See the [config](https://github.com/ibiene-ds/website/blob/master/_config.yml) file for this website.
  - Ctrl + C to stop running the server (only necessary when you edit the config file). 
  - Run `bundle exec jekyll serve` to restart the server to see your changes.
  - Rinse and repeat. <br>
Customization is never really finished but *do* get the blog out - you can always change stuff as inspiration hits. <br>
- **Edit the README.md file**. This is what shows up in your repo in GitHub. You can replace the current contents with a simple paragraph like: *This is my portfolio website using Jekyll and Netlify*. Feel free to add more details. 
- **Edit the index.md file**. This is usually the first page visitors see when they come to your site. It is good to have a short introduction, background etc. <br><br>
With any of these files (except the *config* file), editing the contents would regenerate the site on your local server, so you can see what your changes look like in real-time (almost). Just refresh the local server site after each change and you should be good. 


## Step 5: Your first post/contents of your portfolio
There is usually a **_posts** folder in the hierarchy - you can edit that and start putting content in. The theme creators do an excellent job of including **example posts** - you can edit these and see the changes reflect on your website.  Also, note that Jekyll posts usually follow a convention for naming the posts.

Useful links for writing in markdown (I found inline images quite finicky but finally got the hang of it):
- [Markdown Cheat Sheet](https://www.freecodecamp.org/news/markdown-cheat-sheet/)
- [Markdown Syntax](https://www.markdownguide.org/basic-syntax/)

If you are confused about how to structure content or what projects to add to your portfolio, take a look at some of these amazing portfolios and you'll soon get an idea of how to structure your portfolio. See the links below:
- [Chris Tran Portfolio](https://chriskhanhtran.github.io/portfolio/)
- [Best Analytics Portfolios](https://careerfoundry.com/en/blog/data-analytics/data-analytics-portfolio-examples/)
- [Alexander Kahanek Portfolio](https://alexander-kahanek.github.io/)

_**Word of advice**: Every savant was once an amateur (in other words, do not despise the days of small beginnings). Do not shy away from putting what you consider "small" projects in there -  as you progress in your journey, you can add and subtract from your portfolio. The key is to keep doing projects. The more you do, the better you'll become and the more confident you'll feel - just keep moving._ 

### Optional pretty stuff
#### Shields
So I spent the better part of an hour trying to figure out how to add cool buttons that would link to my GitHub account or a Jupyter Notebook. All of that research (googling) led me to the wonder of **shields** (go to [shields.io](https://shields.io/) to learn more). I have to give a shout-out to Chris Tran here - reading his [blog](https://chriskhanhtran.github.io/portfolio/) helped me out with this idea.

- You can create shields using this format:

`https://img.shields.io.badge/AppName-Message-htmlcolorcode?logo=AppName`

For example, to create a GitHub shield: `https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub`

More formatting options are available on [shields.io](https://shields.io/).

- To create links to another site (like GitHub or a Jupyter Notebook), use the format below:

```
[![](https://img.shields.io/badge/Read_Full_Analysis-blue?)](/blog/enhance-target-accuracy/)
[![](https://img.shields.io/badge/Jupyter-Open_Notebook-blue?logo=Jupyter)](/project-files/enhance-target-accuracy-ml.html)
[![](https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub)](https://github.com/ibiene-ds/enhancing-targeting-accuracy)

```

The code above gives you these pretty buttons/shields

[![](https://img.shields.io/badge/Read_Full_Analysis-blue?)](/blog/enhance-target-accuracy/)
[![](https://img.shields.io/badge/Jupyter-Open_Notebook-blue?logo=Jupyter)](/project-files/enhance-target-accuracy-ml.html)
[![](https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub)](https://github.com/ibiene-ds/enhancing-targeting-accuracy)

*Tip: To add, say two blank spaces before the next shield, modify the code by adding `&nbsp;` after each line:*

```
[![](https://img.shields.io/badge/Read_Full_Analysis-blue?)](/blog/enhance-target-accuracy/) &nbsp; &nbsp;
[![](https://img.shields.io/badge/Jupyter-Open_Notebook-blue?logo=Jupyter)](/project-files/enhance-target-accuracy-ml.html) &nbsp; &nbsp;
[![](https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub)](https://github.com/ibiene-ds/enhancing-targeting-accuracy)

```

[![](https://img.shields.io/badge/Read_Full_Analysis-blue?)](/blog/enhance-target-accuracy/) &nbsp; &nbsp;
[![](https://img.shields.io/badge/Jupyter-Open_Notebook-blue?logo=Jupyter)](/project-files/enhance-target-accuracy-ml.html) &nbsp; &nbsp;
[![](https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub)](https://github.com/ibiene-ds/enhancing-targeting-accuracy)


I find these shields extremely useful - now I can give a very concise summary of a project on my project page, and link interested readers to either the **Full Analysis** or the **Jupyter Notebook** or a **Web App**. In essence, readers can choose the level of detail they want. 

#### Exporting Jupyter Notebooks to .html files
- Go to command line and install **nbconvert** using pip. <br> 
  - `pip install nbconvert` <br>
- To export a notebook, 
  - Change the directory to the folder of interest
    - `cd FolderName` 
  - To export both code and results:
    - `jupyter nbconvert --tohtml notebook-name.ipynb`  
  - To export only results, code will not be present in the html file:
    - `jupyter nbconvert --tohtml --no-input notebook-name.ipynb` 

## Step 6: Push changes to GitHub
You have created some post(s), you love your blog and hopefully, you've added a personal profile about yourself and some nice images to break up the text. Let's push our changes to our GitHub repo. <br>

Open up another command line screen and follow the steps below:
- Navigate to the **website** folder:
  - `cd C:\Desktop\website`
- Push changes to GitHub:
  - `git push origin main`
  or 
  - `git push origin master`
  or simply 
  - `git push`

## Step 7: Deploy online
So far, no one can access your website because it is on your local computer - but what's the point of a blog if only you can read it? So time to deploy.

You can either use **GitHub** or **Netlify** to host your website for free. 

### GitHub
If you have only one site on your account - it is pretty straightforward. 

Simply go to your GitHub repo (**website**). Under *Settings*, change your repo name to *githubusername.github.io*. 
For example, my GitHub user name is **ibiene-ds** so my repo name would be **ibiene-ds.github.io**. This repo name tells GitHub that this is a website (I am sure there are more technicalities to that but that is about it in a nutshell). 

Give it a minute or two, and you'll get a message that says **your site is live!**

![](/assets/img/blog/github-pages-live.png)

If you have more than one site on your GitHub account, there are a couple more steps:
- Name your repo, let's call it **website.**
- Go to **Settings** at the top of the repo page and navigate to **Pages** on the right side of the page.

Under **Build and Deployment**:
- **Source**: Deploy from a branch.
- **Branch**: Choose 'master', '/root'. This means you are deploying from the master branch and the relevant files can be found in the *root* directory.
- **Save**. After a minute or two, there will be a message at the top like this:

<br>  

![add pic of pages]()

**Your site should now be live!**



### Netlify
*Disclosure - I started hosting on GitHub and then it became finicky with a second site. I still don't completely understand it - some sites worked, and some didn't, so I moved to Netlify and wow - so easy!*

- Go to [Netlify](netlify.com) and create an account. Follow the steps to connect your GitHub account. I found this [tutorial](https://www.netlify.com/blog/2016/09/29/a-step-by-step-guide-deploying-on-netlify/) on the Netlify site straightforward and useful.

- Your site is now deployed at a subdomain (netlify.app or netlify.com)

- You can go ahead and change your site name (recommended), or use a custom domain (optional).

## Step 8: Index your site 
Now you have a portfolio website showing your projects. But I quickly learned that deploying a website on GitHub or Netlify does not necessarily mean that search engines like Google or Bing will automatically find it (try it!). 


- Go to **[Google Search Console](https://search.google.com/search-console/about)** and click **Start Now**
- Enter your property name. For this website,  I entered: https://www.ibienenwoko.com
- Now on to **Site Verification**. Google gives you some options for site verification - the most straightforward option (to me) was the first option - **HTML File Upload**. The steps are:
    - Download the .html file, 
    - Upload the .html file to the root directory of your website. 

    On my PC, I have a folder called **website** where I pasted the *html* file and then pushed to my GitHub repository. *See [video](https://support.google.com/webmasters/answer/9008080?hl=en#html_verification) for more information on site verification*. <br> 

    Click **Verify** and you will receive a message almost immediately confirming that you have been verified. 
- **Create/Check Sitemap**. For me, this was a tricky one since I had never even heard about *sitemaps* or *SEO* before this. So, I'll save you some googling. First of all, the sitemap for this site can be accessed by typing: *www.ibienenwoko.com/sitemap.xml* in your browser. <br>
  - Simply add **/sitemap.xml** to the end of your website (either your real site or local server) and you can access your sitemap as well. Local server example: *http://127.0.0.1:4000/sitemap.xml*.


  **Important Checks**:
  - Go to your *_config.yml* file and make sure your *url* and *base url* are **not** commented out. If they are commented out, your sitemap will have '<'loc'>' instead of a proper url. Suffice it to say, Google Search Console will flag errors when you submit that sitemap. See an example of what your config.yml file should look like.
  ![](/assets/img/blog/config.png) 

  - Check that the **Jekyll plugin** to generate sitemaps is active. See highlighted text below. I didn't have to do this part, the theme creator had that already. ![](/assets/img/blog/jekyll-plugins.png)

  - Check that in the front matter of all your posts you want found by a search engine, you have **sitemap: true**. For some reason, I had set mine as false back when I had no clue what a sitemap was. ![](/assets/img/blog/sitemap-true.png) <br> <br>

  If you have all these checked off, you have a sitemap. Check this by going to your *www.websitename.com/sitemap.xml.* 

5. **Submit Sitemap**. Back to Google Search Console. Go to *Sitemaps* on the left side and add a new sitemap. Your website or property name should be there already - just add `sitemap.xml` and hit **Submit**. <br>

![](/assets/img/blog/sitemap.png)

If you completed the checks above, there should be no errors. 

![](/assets/img/blog/sitemap-success.png)

Now, you wait for 2 - 5 days for Google to index your site and voila! You are on Google.

These are links to some resources I found helpful. 

- [Get your Jekyll pages on Google](https://victor2code.github.io/blog/2019/07/04/jekyll-github-pages-appear-on-Google.html)
- [Google Analytics on Jekyll](https://desiredpersona.com/google-analytics-jekyll/)
- [How to create a sitemap on Jekyll](https://www.youtube.com/watch?v=kiBtQClK-XQ)

And you are done! You have a portfolio website - now just keep doing projects and adding to it!














