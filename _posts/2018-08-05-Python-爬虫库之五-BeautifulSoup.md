---            
title:  Python-爬虫库之五-BeautifulSoup
date:   2018-08-05 12:00:00
---
# Python-爬虫库之五-Beautiful-Soup

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

  - `.`   # 代表class

  - `>`   # 两边空一格，左父右子

  - `soup.select('标签')`   用 BeautifulSoup 查找元素`imgs = soup.select('p.image > a > img')`

  - 已经得到了标签的内容，那么问题来了，我们要想获取标签内部的文字怎么办呢？很简单，用 `.string `即可 。 

    例：`print soup.p.string `  p 是节点。

  - 





> {{ site.prompt }}

<div  align="center">
<img src="https://rengui520.github.io/images/wechart.jpg" width = "200" height = "200"/>