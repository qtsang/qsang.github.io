---
layout: post
title: Mac下使用Jrebel插件 
categories: Mac软件
description: Mac下使用Jrebel插件。
keywords: Mac,Jrebel

---

Jrebel是一种生产工具，可以提高开发效率，本文主要讲解如何在Mac下通过Idea插件破解使用Jrebel插件。

一、在IDEA的Preference -> Plugins中搜索Jrebel安装，然后重启IDEA，安装过程省略。



二、下载反向代理工具

访问此 [下载链接](https://github.com/ilanyu/ReverseProxy/releases/tag/v1.4) ，下载ReverseProxy_darwin_amd64 文件。

> 注意：Mac用户使用Safari下载，不要用Chrome，否则下载之后会把.dms后缀名去掉

三、运行反向代理工具

Mac用户打开终端，输入命令如下：

```
#为该文件赋予可执行权限
chmod 777 '文件路径'
# 执行该文件
$bash '文件路径'
```

> **Tips：**
>
> - 在Finder中选中反向代理工具文件后，按 Command + Option + C 即可复制文件路径；
> - 文件路径名中请不要带空格，否则无法找到该文件。
> - 运行工具后请不要关闭终端或使用 Control + C 中断执行。

四 配置激活JRebel插件

1、点击 [下载链接](https://www.guidgen.com/) 生成自己的guid复制下来

2、在IDEA中激活JRebel

选中 Team URL (connect to online licensing service) 选项

```
地址栏输入：http://127.0.0.1:8888/ + “刚才复制的guid”
Email随意填写符合格式的邮箱地址即可
```

3、 离线使用JRebel插件

在Preference -> JRebel设置中，点击Work offline按钮，JRebel插件可以离线运行了。可以看到JRebel的过期时间，一般是半年，半年过期后，使用本文描述的方式再执行一次就可以了

五、设置Jreble

激活以后就可以按照向导使用了，如果没有按照向导，如果不按照向导，一定要把自动编译打开，不然无法实现自动部署。