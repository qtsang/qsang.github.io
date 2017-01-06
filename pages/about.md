---
layout: page
title: About
description: 编码为乐
keywords: qtsang, 码乐
comments: true
menu: 关于
permalink: /about/
---

我是码乐，知之者不如好之者，好之者不如乐之者。

仰慕「优雅编码的艺术」。

## 坚信

* 熟能生巧
* 努力改变人生

## 联系

* GitHub：[@qtsang](https://github.com/qtsang)
* 博客：[{{ site.title }}]({{ site.url }})

## Skill Keywords

#### Software Engineer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_software_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>

#### Mobile Developer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_mobile_app_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>

#### Windows Developer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_windows_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>
