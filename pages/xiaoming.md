---
layout: xiaoming
title: 被发现了么Σ(・ω・ノ)ノ
description: 并没什么用的关键词描述。
keywords: 王小明, 小明
permalink: /xiaoming/
---
<ul>
{% for xiaoming in site.xiaoming %}
{% if xiaoming.title != "xiaoming Template" %}
<li><a href="{{ site.url }}{{ xiaoming.url }}">{{ xiaoming.title }}</a></li>{% endif %}{% endfor %}
<!--xiaoming-->
</ul>
