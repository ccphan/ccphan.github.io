---
layout: post
title: "Setting up an Octopress Blog"
date: 2014-09-02 15:08:42 +0900
comments: true
categories: [Ruby, Rails, Octopress, Heroku] 
---
I'm starting this blog to document my findings and trials with getting started with web development via Ruby Rails.  This is my first foray into web development and my first ever blog.

I'm using Octopress as my blogging platform.  Fittingly it's built from Rails around Jekyll.  Deployment with be on Heroku.  Some of resouces used to help setup this blog:

> * [http://www.jackiejohnston.us/blog/setting-up-an-octopress-blog-on-heroku/](http://www.jackiejohnston.us/blog/setting-up-an-octopress-blog-on-heroku/ "jackiejohnston")  
> * [http://octopress.org/docs/setup/](http://octopress.org/docs/setup/)  

## Octopress Command Reference ##
### Creating a Post ###
```
$ rake new_post["title"]  
$ rake new_post["Setting up a Blog"]  
```
### Converting Markdown to html ###
```
$ rake generate  
```
### Preview ###
```
$ rake preview  
```
### Deploy on Heroku and view ###
Create a git remote name "heroku" to point to you git respository on Heroku:
```
$ git config branch.master.remote heroku  
```

Commit and deploy onto Heroku:
```
$ git add .
$ git commit -m "some update"
$ git push heroku master    
$ heroku open  
```

## Markdown ##
The source posts files genereated are in [Markdown](http://en.wikipedia.org/wiki/Markdown/ "Markdown") format by default.  

In terms of styling, take a look at [Markdown reference](http://daringfireball.net/projects/markdown/basics).  Also Octopress comes bundled with it's own code snippets mark up.  Check it out [here](http://octopress.org/docs/blogging/code/).