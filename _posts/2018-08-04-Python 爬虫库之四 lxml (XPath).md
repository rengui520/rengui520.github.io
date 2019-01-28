---             
title:  Python-爬虫库之四-lxml-(XPath)
date:   2018-08-04 12:00:00
---
# Python 爬虫库之四 lxml (XPath)

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

- lxml (XPath)

  - /tbody  标签需删除 

  - 要获取标题文本，所以 xpath 表达式要追加`/text() `

  - xpath 的简单用法:

    ```
    from lxml import etree
    
    element = etree.HTML("html字符串")
    #s=etree.HTML(源码) #将源码转化为能被XPath匹配的格式
    
    element.xpath("")
    #s.xpath(xpath表达式) #返回为一列表,
    ```

    

  - 基础语法：

  	```
  	/    #从当前节点选取直接子节点
  	//  #从当前节点选取子孙节点
  	.  #选取当前节点
  	..   #选取当前节点的父节点
  	@  #选取属性
    
  	//title[@lang='eng']   #选择所有名称为 title ，同时属性 lang 的值为 eng 的节点
  	//*[@lang='eng']       #选择属性 lang 的值为 eng 的节点
  	```

① 选择节点(标签)

ⓐ /html/head/meta：能够选中 html 下的 head 下的所有的 meta 标签

② //：能够从任意节点开始选择

ⓐ //li：当前页面上的所有的 li 标签

ⓑ /html/head/link：head 下的所有的 link 标签

③ @ 符号的用途

ⓐ 选择具体某个元素：//div[@class='feed-infinite-wrapper']/ul/li #选择 class='feed-infinite-wrapper'的 div 下的 ul 下的 li 

ⓑ a/@href：选择 a 的 href 的值

④ 获取文本：/a/text()

ⓐ  /a/text()：获取 a 下的文本

ⓑ  /a//text()：获取 a 下的所有的文本

⑤ 点前

ⓐ  "./a" 当前节点下的 a 标签

> {{ site.prompt }}

<div  align="center">
<img src="https://rengui520.github.io/images/wechart.jpg" width = "200" height = "200"/>