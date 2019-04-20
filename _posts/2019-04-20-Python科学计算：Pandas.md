---              
title:  Python科学计算：Pandas
date:   2019-04-20 12:00:00
tag:    数据分析
---
Series 和 DataFrame 这两个核心数据结构，他们分别代表着一维的序列和二维的表结构。      

Series 是个定长的字典序列。说是定长是因为在存储的时候，相当于两个 ndarray，这也是和字典结构最大的不同。因为在字典的结构里，元素的个数是不固定的。      

Series 有两个基本属性：index 和 values。在 Series 结构中，index 默认是 0,1,2,……递增的整数序列，当然我们也可以自己来指定索引，比如 index=[‘a’, ‘b’, ‘c’, ‘d’]。










