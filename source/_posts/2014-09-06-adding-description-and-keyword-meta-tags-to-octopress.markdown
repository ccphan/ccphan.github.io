---
layout: post
title: "Adding  description and keywords meta tags to Octopress"
date: 2014-09-06 00:23:58 +0900
comments: true
categories: Octopress 
description: Adding meta description and keywords Octopress
keywords: Octopress, meta tags
---
Octopress does not setup description and keyword meta tags.  So you'll need to make a few changes.
<!-- more -->

In the _config.yml add:

{% codeblock _config.yml %}
url: http://www.mysite.com
title: My Blog
subtitle: Just another blog
author: My Name
simple_search: https://www.google.com/search
description: Rails blog
keywords: key1, key2, key3
{% endcodeblock %}

In the post changes you'll need to add the 'description' and 'keywords' field manually to the YAML frontmatter (not investigated how to have this populated automatically).  

Then to have these displayed with your home page and post page you'll need to modify `source/_includes/head.html`.

Before:
{% codeblock lang:html source/_includes/head.html %}
{% raw %}
<meta name="author" content="{{ site.author }}">
{% capture description %}{% if page.description %}{{ page.description }}{% else %}{{ content | raw_content }}{% endif %}{% endcapture %}
<meta name="description" content="{{ description | strip_html | condense_spaces | truncate:150 }}">
{% if page.keywords %}<meta name="keywords" content="{{ page.keywords }}">{% endif %}
{% endraw %}
{% endcodeblock %}

After:
{% codeblock lang:html source/_includes/head.html %}
{% raw %}
<meta name="author" content="{{ site.author }}">
{% capture description %}{% if page.description %}{{ page.description }}{% else %}{{ content | raw_content }}{% endif %}{% endcapture %}
<meta name="description" content="{{ description | strip_html | condense_spaces | truncate:150 }}">
{% if page.keywords %}<meta name="keywords" content="{{ page.keywords }}">{% endif %}
{% endraw %}
{% endcodeblock %}