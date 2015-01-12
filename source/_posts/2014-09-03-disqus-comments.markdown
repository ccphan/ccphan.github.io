---
layout: post
title: "Disqus Comments"
date: 2014-09-03 19:11:11 +0900
comments: true
categories: [Octopress, Disqus] 
description: Setting up Disqus on Octopress
keywords: Octopress, Disqus
---
Octopress generates static sites.  For your site to support comments you will need to use a third party service to host your comments.

Octopress has plugin support to _Disqus_ and it's pretty easy to setup.
<!-- more -->
### 1. Signup to Disqus
Head to [disqus](https://disqus.com/ "Disqus") and sign yourself up.  Keep note of the _site short name_ they provide.

### 2. Edit _config.yml

{% codeblock lang:ruby _config.yml %}
# Disqus Comments
disqus_short_name: enter_short_name_here
disqus_show_comment_count: true
{% endcodeblock %}


That should be pretty much it.