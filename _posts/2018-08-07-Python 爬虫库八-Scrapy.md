---             
title:  Python 爬虫库(7)-Scrapy
date:   2018-08-07 12:00:00
tag:    Spider
---
# Python 爬虫库(7)-Scrapy

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

<head><link rel="stylesheet" href="../css/rouge.css"></head>
在我们编写爬虫之前，先了解一下`scrapy`的爬取机制，`scrapy`和绝大多数的爬虫喜欢用繁琐的正则表达式不同，他更喜欢使用的`xpath`和`CSS`的类来搜索他要的信息，笔者试过很多正则表达式的框架，首先正则表达式本来就是个很繁琐的东西，而且经常会出错，重写正则表达式就会耗去大量的开发时间，而`XPath`的本就是为了解析`HTML`和`XML`而做的，非常方便，

不懂`xpath`的同学可以点这里：[xpath教程](http://www.w3school.com.cn/xpath/)

### 安装

`pip3 istall scrapy`

`conda install scrapy `

### 使用

在命令行中切换到要存储的位置 `cd /d D:/xxx`

创建Scrapy项目 `scrapy startproject xxx`

### 编写

设置 item.py : 十分的简单，只需要将希望获取的字段名填写进去。

然后在 spiders 文件夹中新建一个与项目同名的爬虫文件 xxx.py 

然后编写 piplines.py ，处理 spider 爬到的内容，定义我们的储存。如保存到数据库还是保存到普通文件夹中。

最后设置 setting.py 

```
ROBOTSTXT_OBEY = True 设置为 False

将下列部分的注释去掉
ITEM_PIPELINES = {
    'dingdian.pipelines.DingdianPipeline': 300,
}

等
```

### 运行程序

在项目目录下打开终端，并执行以下命令。

 `scrapy crawl 项目设置的爬虫名字` 
或者 `scrapy crawl 项目设置的爬虫名字 -o item.json`

第二条命令中，我们没有 pipelines.py 中将爬取结果进行存储，所以我们使用 scrapy 提供的导出数据命令，将 15 条电影信息导出到名为 items.json 文件中。

其中 vmoive 为刚才在 爬虫文件 中定义的 name 属性的值。

友链：

<p><a href="https://mp.weixin.qq.com/s?__biz=MzIwODY1MDc1NQ==&mid=2247484072&idx=1&sn=3643b6368193f16d3451a473fde2135d&chksm=977e95c4a0091cd275098e4e1e916cbdbf80a4d399ac388d9476d25b4826aabdcdce97a109c5&scene=21#wechat_redirect">scrapy初探</a></p> 

> {{ site.prompt }}

<div  align="center">
<img src="https://rengui520.github.io/images/wechart.jpg" width = "200" height = "200"/>