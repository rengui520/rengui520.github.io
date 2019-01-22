---            
title:  Python-学习之旅-3-模块
date:   2018-08-09 12:00:00
---
# Python-学习之旅-3-模块
***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

模块基本上就是一个包含了所有你定义的函数和变量的文件。为了在其他程序中重用模块，模块的文件名必须以 .py 为扩展名。

记住这个模块应该被放置在我们输入它的程序的同一个目录中

1. `import` 导入库

2. `from...import` 语句  Python 的 `from` 语句让你从模块中导入一个指定的部分到当前的命令空间中，语法如下：

   ```python  
   from bs4 import Beautiful Soup
   ```

3.   `From…import*` 语句  把一个模块的所有内容全部导入到当前的命名空间也是可行的，只需使用如下声明：    

   ```python
   from modname import*
   ```

   这提供了一个简单的方法来导入一个模块中的所有项目。然而这种声明不该被过多地使用。

4. 
> {{ site.prompt }}

<div  align="center">
<img src="https://xuujii.github.io/images/wechart.jpg" width = "200" height = "200"/>