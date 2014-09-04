---
layout: post
title: "Setting up a Octopress Blog"
date: 2014-09-02 15:08:42 +0900
comments: true
categories: [Octopress, Heroku, markdown]
description: Setting up Octopress
keywords: Octopress, Heroku, Rails 
---
Get blogging with Octopress.  It has a number of advantages:  

    *  Jekyll based and Git-system backed  
    *  Markdown supported  
    *  Quick and easy to deploy
    *  Stylish code snippet markup  
    *  Supports many plugins driven by Jekyll liquid templating  

<!-- more -->
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

If you need tips on setting up Heroku check out the guide [here]({% post_url 2014-09-03-getting-started-with-heroku %} "Guide to setting up Heroku").

### 8. Deploying on GitHub (Alternative)
The workflow is slightly different when chosing to deploy onto GitHub.  Initial development work is done on a `source` branch and when everything is good the generated content is deployed onto a `master` branch on GitHub which is like the public directory on a web server.

#### Create a new GitHub repository
The format should be `username.github.io`.  You'll be able to access your site with the url `http://username.github.io`.

#### Run the Octopress setup tasks

    $ rake setup_github_pages

The rake task will ask you for a URL of the Github repo. Copy the SSH or HTTPS URL from your newly created repository (e.g. git@github.com:username/username.github.io.git) and paste it in as a response.

This will:

- Ask for and store your Github Pages repository url.
- Rename the remote pointing to imathis/octopress from 'origin' to 'octopress'
- Add your Github Pages repository as the default origin remote.
- Switch the active branch from master to source.
- Configure your blog's url according to your repository.
- Setup a master branch in the _deploy directory for deployment.

#### Deploy it

    $ rake generate
    $ rake deploy

This will copy generated files to `_deploy/` directory, git add, git commit and git push to master branch.  You'll be able to view the site at `http://username.github.io`.

#### Checking in your local source changes
Going forward remember to check in your local changes.

    $ rake generate
    $ git add .
    $ git commit -m 'your message'
    $ git push origin source

#### Custom Domains
If you need to register a new domain name you can get one at [namecheap](https://www.namecheap.com/ "namecheap").

If you are using namecheap you will need to head to `Manage Domains > Modify Domain` and click onto the `All Host Records`. Edit with the following:

        Host Name: @
        IP Address/URL: 192.30.252.153
        Record Type: A (Address)

        Host Name: www
        IP Address/URL: username.github.io
        Record Type: CNAME (Alias)

Create a `CNAME` file under your blog's `source/` directory and add a line with your custom domain `customdomain.com`.

Note it may take some time for your DNS changes to propagate.

### Additonal Resources
[http://octopress.org/docs/setup/](http://octopress.org/docs/setup/)