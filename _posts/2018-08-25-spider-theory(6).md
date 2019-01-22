---             
title:  Python 爬虫库之六-pyquery
date:   2018-09-06 12:00:00
---
# Python 爬虫库之六-pyquery
***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

# 初始化

使用 pyquery 之前，必须初始化。它的初始化方式有多种，比如直接传入字符串、传入URL、传入文件名等

#### 字符串初始化

```python
from pyquery import PyQuery as pq
doc = pq(html)
print(doc('li'))
```

首先引入 PyQuery 这个对象，取别名为 pq 。然后声明了一个长 HTML 字符串，并将其当作参数传递给 PyQuery 类，这样就成功完成了初始化。接下来，将初始化的对象传入 CSS 选择器(这里，我们传入 li 节点，这样就可以选择所有的 li 节点)。

#### URL 初始化

#### 文件初始化



# 查找节点

#### 子节点

`find()`方法

#### 父节点

`parent()`方法

#### 兄弟节点

`siblings()`方法

# 遍历

调用`item()`方法

# 获取信息

#### 获取属性

调用`attr()`方法

#### 获取文本

调用`text()`方法

> {{ site.prompt }}

<div  align="center">
<img src="https://xuujii.github.io/images/wechart.jpg" width = "200" height = "200"/>