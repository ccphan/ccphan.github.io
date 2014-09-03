---
layout: post
title: "Setting up a Octopress Blog"
date: 2014-09-02 15:08:42 +0900
comments: true
categories: [Octopress, Heroku, markdown] 
---
Get blogging with Octopress.  It has a number of advantages:  

    *  Jekyll based and Git-system backed  
    *  Markdown supported  
    *  Quick and easy to deploy (Rails)  
    *  Stylish code snippet markup  
    *  Supports many plugins driven by Jekyll liquid templating  

## Setup Guide

### 1. Download Octopress
```
$ git clone git://github.com/imathis/octopress.git octopress
$ cd octopress
```

### 2. Install Octopress
```
$ gem install bundler
$ bundle install
$ rake install
```

### 3. Configuration
#### i. Edit `.gitignore`  

Remove lines: `public` and `Gemfile.lock`.

#### ii. Configure the `_config.yml`

Basic settings:

{% codeblock lang:ruby _config.yml %}
url: http://www.mysite.com
title: My Blog
subtitle: Just another blog 
author: My Name
simple_search: https://www.google.com/search
description: Rails blog
{% endcodeblock %}

You can add third party feeds to the sidebar by appending the relevant html to the `default_asides:` list.

{% codeblock lang:ruby _config.yml %}
default_asides: [asides/recent_posts.html, asides/github.html, asides/delicious.html, asides/pinboard.html, asides/googleplus.html, asides/twitter.html]
{% endcodeblock %}

#### iii. Twitter feed

To pull in twitter feeds you will need to grab the generated widget code from the Twitter site and create a `asides/twitter.html` file like below:

{% codeblock lang:html source/_includes/asides/twitter.html %}
<section>
  <h1>Twitter</h1>
  <!-- PASTE THE WIDGET CODE HERE -->
</section>
{% endcodeblock %} 

Then paste the twitter widget code into stated section. 

#### iv. Gemfile

Add the `:production` group for when this eventually gets deployed onto Heroku.

{% codeblock lang:ruby Gemfile %}
group :development, :production do
  gem 'rake', '~> 10.0'
  gem 'jekyll', '~> 2.0'
  gem 'octopress-hooks', '~> 2.2'
  ...
end
{% endcodeblock %} 

### 4. Creating a Post
```
$ rake new_post["Setting up a Blog"]  
# Creates source/_posts/2014-09-02-setting-up-a-blog.markdown
```
The source posts files genereated are in [markdown](http://en.wikipedia.org/wiki/Markdown/ "markdown") format by default.  

In terms of styling, take a look at [markdown reference](http://daringfireball.net/projects/markdown/basics).  Also Octopress comes bundled with its own code snippets markup.  Check it out [here](http://octopress.org/docs/blogging/code/).

### 5. Creating an About Page
```
$ rake new_page[About]
# creates source/about/index.markdown
```
_OR_
```
$ rake new_page[About/page.html]
# creates source/about/page.html
```
To add a nav menu link to this page you will need to edit the `custom/navigation.html` to look something like:
{% codeblock lang:html source/_include/custom/navigation.html %}
<ul class="main-navigation">
  <li><a href="{{ root_url }}/">Blog</a></li>
  <li><a href="{{ root_url }}/blog/archives">Archives</a></li>
  <li><a href="{{ root_url }}/about">About</a></li>
</ul>
{% endcodeblock %}


### 6. Converting Markdown to HTML and preview
```
$ rake generate  
$ rake preview  
```
Head to `http://localhost:4000` to preview site.

### 7. Deploy on Heroku and view
Create a git remote name "__heroku__" to point to you git respository on Heroku:
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

If you need tips on setting up Heroku check out the guide [here](http://somelink.com "Guide to setting up Heroku").

Also you can find more details on setting up your own domain name [here](http://somelink.com "Setting up your domain name").

### Additonal Resources
[http://octopress.org/docs/setup/](http://octopress.org/docs/setup/)