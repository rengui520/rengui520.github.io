---             
title:  Python 爬虫库之六-pyquery
date:   2018-08-06 12:00:00
tag:    Spider
---
# Python 爬虫库之六-pyquery

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

<head><link rel="stylesheet" href="../css/rouge.css"></head>
强大又灵活的网页解析库。使用 pyquery 之前，必须初始化。它的初始化方式有多种，比如直接传入字符串、传入URL、传入文件名等。

1.
初始化
字符串初始化

```python
html = '''
<div class="wrap">
<div id="container">
    <ul class="list">
        <li class="item-0">first item</li>
        <li class="item-1"><a href="link2.html">second item</a></li>
        <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
        <li class="item-1 active"><a href="link4.html">fourth item</a></li>
        <li class="item-0"><a href="link5.html">fifth item</a></li>
    </ul>
</div>
</div>
'''
from pyquery import PyQuery as pq  #用pq代替PyQuery这个类。
doc = pq(html)  #声明了一个长 HTML 字符串，并将其当作参数传递给 PyQuery 类，这样就成功完成了初始化。
print(doc('li'))   #将初始化的对象传入 CSS 选择器(这里，我们传入 li 节点，这样就可以选择所有的 li 节点)。
```
输出结果：
```
<li class="item-0">first item</li>
        <li class="item-1"><a href="link2.html">second item</a></li>
        <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
        <li class="item-1 active"><a href="link4.html">fourth item</a></li>
        <li class="item-0"><a href="link5.html">fifth item</a></li>
```

2.
CSS 选择器：
选择 id，则用 # 代替 id；选择 class，则用 . 代替；选择标签，直接输入标签名即可。
上述输出结果也可用下列语句代替。
```python
print(doc('#container .list li'))
```

3.
查找元素

3.1 子节点

利用 `find()`方法即可查找子节点。而 `children()` 方法则是查找直接子节点。
```python
items = doc('.list')  #选择ul 标签的所有内容。
print(type(items))   #打印ul标签的类型(<class 'pyquery.pyquery.PyQuery'>)
lis = items.find('li')   #打印ul标签的子标签li的内容。
print(lis)
```
```python
lis = items.children() #查找直接子元素。
lis = items.children('.active') #当然，也可给children传入参数，进一步查找。
```
3.2 父节点

利用 `parent()`方法即可查找父节点。 `parents()`方法查找所有祖先节点。
```python
items = doc('.list') 
container = items.parent()   #获取ul标签的父节点div的所有内容。
```
```python
container = items.parents()  #查找ul标签的祖先节点，有多少个祖先节点便输出多少次。

container = items.parents('.wrap') #当然，也可给parents传入参数，指定哪一层祖先节点。
```

3.3 兄弟节点

利用 `siblings()`方法即可查找兄弟节点。
```python
li = doc('.list .item-0.active')  #list后边有一个空格，表示选择其里边的内容；activer前边没空格，表示与前边内容并列的意思。
print(li.siblings()) #输出除了本身外的兄弟元素。

print(li.siblings('.active')) #也可传入参数指定兄弟节点。
```

4.
遍历

查找多个元素时，可以遍历查找，以防漏查。调用 `item()` 方法即可。
```python
lis = doc('li').items()  #利用.items()方法生成一个产生器。
print(type(lis))  #使用items()方法后类型为<class 'generator'>
for li in lis:
    print(li)
```

5.
获取信息

5.1 获取属性

调用 `attr()` 方法
```python
a = doc('.item-0.active a')
print(a)
print(a.attr('href'))  #获取属性值
print(a.attr.href)    #与上边结果一样

输出结果：
<a href="link3.html"><span class="bold">third item</span></a>
link3.html
link3.html
```

5.2 获取文本

调用 `text()` 方法

```python
a = doc('.item-0.active a')
print(a)
print(a.text())

输出结果：
<a href="link3.html"><span class="bold">third item</span></a>
third item
```

5.3 获取 HTML
获取这个节点内部的 HTML 文本，就需要用 html() 方法。
当选中的结果是多个节点时，html() 方法返回的是第一个节点内部的 HTML 文本。
```python
li = doc('.item-0.active')
print(li)
print(li.html())

输出结果：
<li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
        
<a href="link3.html"><span class="bold">third item</span></a>
```

6.
节点（DOM）操作
6.1 removeClass()、addClass()方法可以动态改变节点的 class 属性。
```python
li = doc('.item-0.active')
print(li)
li.removeClass('active')  #将active这个class移除
print(li)
li.addClass('active')   #将active这个class添加回来
print(li)

输出结果：
<li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
        
<li class="item-0"><a href="link3.html"><span class="bold">third item</span></a></li>
        
<li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
```

6.2 attr、css、text、html 方法
```python
li = doc('.item-0.active')
print(li)
li.attr('name','link')  #利用 attr 修改属性，当属性不存在时，自动添加；当属性存在时，则修改为设定值。
print(li)
li.css('font-size','14px')  #利用 css修改style属性
print(li)
li.text('changed item')  #利用text修改文本
print(li)
li.html('<span>changed item</span>')  #利用html修改节点内部的内容
print(li)

输出结果：
<li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
        
<li class="item-0 active" name="link"><a href="link3.html"><span class="bold">third item</span></a></li>
        
<li class="item-0 active" name="link" style="font-size: 14px"><a href="link3.html"><span class="bold">third item</span></a></li>
        
<li class="item-0 active" name="link" style="font-size: 14px">changed item</li>
        
<li class="item-0 active" name="link" style="font-size: 14px"><span>changed item</span></li>
```
所以说，如果 attr() 方法只传入第一个参数的属性名，则是获取这个属性值；如果传入第二个参数，可以用来修改属性值。text() 和 html() 方法如果不传参数，则是获取节点内纯文本和 HTML 文本，如果传入参数，则进行赋值。

6.3 remove() 方法移除相关信息。
```python
html = '''
<div class="wrap">
    Hello,World
    <p>This is a paragraph.</p>
</div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
wrap = doc('.wrap')
print(wrap.text())
wrap.find('p').remove()  #选中 p 节点，调用remove() 方法将其移除。
print(wrap.text())  #利用 text() 获取文本 Hello,World

输出结果：
Hello,World
This is a paragraph.
Hello,World
```

> {{ site.prompt }}

<div  align="center">
<img src="https://rengui520.github.io/images/wechart.jpg" width = "200" height = "200"/>