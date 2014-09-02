---
layout: post
title: "Setting up an Octopress Blog"
date: 2014-09-02 15:08:42 +0900
comments: true
categories: [Octopress, Heroku] 
---
Get blogging with Octopress.  It has a number of advantages:
* Jekyll based and Git-system back
* posts and pages can be written in Markdown
* quick and easy to deploy (Rails)
* code snippet mark up
* supports many plugins driven my Jekyll liquid templating

## Setup Guides ##

* [http://www.jackiejohnston.us/blog/setting-up-an-octopress-blog-on-heroku/](http://www.jackiejohnston.us/blog/setting-up-an-octopress-blog-on-heroku/ "jackiejohnston")  
* [http://octopress.org/docs/setup/](http://octopress.org/docs/setup/)  

## Octopress Command Reference ##
### Creating a Post and Page###
```
$ rake new_post["Setting up a Blog"]  
# Creates source/_posts/2014-09-02-setting-up-a-blog.markdown
```
### Creating a Page ###
```
$ rake new_page[awesome-page]
# creates /source/awesome-page/index.markdown
 
$ rake new_page[awesome-page/page.html]
# creates /source/awesome-page/page.html
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