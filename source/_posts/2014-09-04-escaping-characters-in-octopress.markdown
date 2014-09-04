---
layout: post
title: "Escaping characters in Octopress"
date: 2014-09-04 19:38:44 +0900
comments: true
categories: [Octopress]
description: escaping characters in Octopress
keywords: Octopress, octopress-escape-code
---
To ensure that a particular content block won't be parsed by Liquid and displayed 'as is' you can enclose the block contents in `<% raw %>` and `<% endraw %>` tag.

For example you can display xml snippet like (replace `[` with `{` in example):

{% codeblock lang:xml %}
[% codeblock lang:xml file.xml %]
  [% raw %]
    {% raw %}<entry>
    ...
    <content type="html"><![CDATA[{{ post.content | expand_urls: site.url | markdownize | cdata_escape }}]]></content>
    </entry>{% endraw %}
  [% endraw %]
[% endcodeblock %]
{% endcodeblock %}

It'll appear like:

{% codeblock lang:xml file.xml %}
{% raw %}
<entry>
...
<content type="html"><![CDATA[{{ post.content | expand_urls: site.url | markdownize | cdata_escape }}]]></content>
</entry>
{% endraw %}
{% endcodeblock %}
