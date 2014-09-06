---
layout: post
title: "Linking to internal posts in Octopress"
date: 2014-09-04 19:09:31 +0900
comments: true
categories: [Octopress]  
description: Linking to internal posts with post_url in Octopress
keywords: Octopress
---
You can use the `post_url` to link to your internal posts:

{% raw %}
        [link_text]({% post_url YYYY-MM-DD-your-internal-post %} "hover text")
{% endraw %}
<!-- more -->
However when running _rake generate_ I hit this kind of error:

{% raw %}
    Liquid Exception: Tag '{%%20\post_url\%20YYYY-MM-DD-your-internal-post%20%}' was not properly terminated with regexp: /\%}/ in atom.xml
{% endraw %}

The fix appears to be replace "markdownify" to "markdownize" in the _includes/custom/category_feed.xml:

{% codeblock lang:xml source/_includes/custom/category_feed.xml %}
{% raw %}
<entry>
...
<content type="html"><![CDATA[{{ post.content | expand_urls: site.url | markdownize | cdata_escape }}]]></content>
</entry>
{% endraw %}
{% endcodeblock %}
