---
layout: page
title: About
description: 积累 成长
keywords: Le Yao, 姚乐
comments: true
menu: 关于
permalink: /about/
---

我是姚乐，云软件工程师。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
