---              
title:  Python科学计算：用NumPy快速处理数据
date:   2019-03-13 12:00:00
tag:    数据分析
---

<head><link rel="stylesheet" href="../css/rouge.css"></head>
axis=0 是跨行（纵向），axis=1 是跨列（横向）

## Numpy入门
### ndarray 对象
ndarray 实际上是多维数组的含义。在 NumPy 数组中，维数称为秩（rank），一维数组的秩为 1，二维数组的秩为 2，以此类推。在 NumPy 中，每一个线性的数组称为一个轴（axes），其实秩就是描述轴的数量。

### Array 的创建及访问 
```python
import numpy as np
a = np.array([1, 2, 3])   # 直接通过 array 函数创建数组
b = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
b[1,1]=10       # 行跟列的下标是从 0 开始计的
print(a.shape)    # 返回行列数
print(b.shape) 
print(a.dtype)    # 类型。类型不一致，取精确度最高的
print(b)
print(b.size)   # 元素个数

结果：
(3,)
(3, 3)
int32
[[ 1  2  3]
 [ 4 10  6]
 [ 7  8  9]]
9
```

```python
c = np.arange(1, 10, 2)  #左包括，右不包括。后一个参数为递增间隔
print(c)
d = np.zeros(5)
print(d)  # 全零一维矩阵
f = np.zeros([2, 3])  #全零二维矩阵
print(f)
e = np.eye(5)  #产生单位矩阵
print(e)

结果：
[1 3 5 7 9]

[0. 0. 0. 0. 0.]

[[0. 0. 0.]
 [0. 0. 0.]]
 
 [[1. 0. 0. 0. 0.]
 [0. 1. 0. 0. 0.]
 [0. 0. 1. 0. 0.]
 [0. 0. 0. 1. 0.]
 [0. 0. 0. 0. 1.]]
```

```python
g = np.arange(1, 10)   
print(g)
print(g[1])     #访问第二个元素，从零开始数
print(g[1:5])   #访问范围。左包括，右不包括 

h = np.array([[1, 2, 3],[4, 5, 6],[7, 8, 9]])    # 创建三维数组
print(h[1][0])     #访问第二行第零个  行跟列从零开始数
print(h[1, 0])     #同上
print(h[:2,1:])  #第二行截至，第二列开始

结果：
[1 2 3 4 5 6 7 8 9]
2
[2 3 4 5]

4
4
[[2 3]
 [5 6]]
```

### 数组与矩阵运算
```python
i1 = np.random.randn(10)  #创建一个随机一维数组,值符合正态分布
print(i1)
i2 = np.random.randint(10)  #生成一个 10 以内的随机数，包括 0-9
print(i2)
i3 = np.random.randint(10, size=(2, 3))  #利用参数 size 创建多维数组
print(i3)
i4 = np.random.randint(10, size=20)  #创建一维数组，10 以内，20 个数
print(i4)
i5 = np.random.randint(10, size=20).reshape(4, 5)  #把一维数组变为多维数组，
print(i5)

结果：
[-0.4799064   0.90009812 -0.53315152 -0.33763872  0.23889252  1.23343036
 -0.55018753  1.47400788  1.30866825 -0.30432421]
 
1

[[0 3 9]
 [5 6 2]]
 
[4 4 1 2 4 2 2 0 7 0 0 1 6 0 8 6 1 8 9 5]

[[5 5 1 7 7]
 [2 3 4 1 4]
 [9 2 6 0 4]
 [4 8 1 1 8]]
```

```python
h = np.random.randint(10, size=20).reshape(4, 5)
g = np.mat([[1, 2, 3],[4, 5, 6]])   # 创建矩阵
print(g)
print(np.mat(h))  # 将数组改为矩阵

结果：
[[1 2 3]
 [4 5 6]]
 
[[7 0 2 2 6]
 [5 1 7 6 6]
 [2 3 8 7 9]
 [2 0 3 3 3]]
```

两个数组之间的加、减、乘、除、求 n 次方和取余数。
```python
x1 = np.arange(1,11,2)
x2 = np.linspace(1,9,5)
print(x1)
print(x2)
print (np.add(x1, x2))
print (np.subtract(x1, x2))
print (np.multiply(x1, x2))
print (np.divide(x1, x2))
print (np.power(x1, x2))
print (np.remainder(x1, x2))

结果：
[1 3 5 7 9]
[1. 3. 5. 7. 9.]
[ 2.  6. 10. 14. 18.]
[0. 0. 0. 0. 0.]
[ 1.  9. 25. 49. 81.]
[1. 1. 1. 1. 1.]
[1.00000000e+00 2.70000000e+01 3.12500000e+03 8.23543000e+05
 3.87420489e+08]
[0. 0. 0. 0. 0.]
```
```python
a = np.mat(np.random.randint(10, size=20).reshape(4, 5))
b = np.mat(np.random.randint(10, size=20).reshape(5, 4))     # 乘法需a的行数与b的列数相同才行
print(a)
print(b)
print(a*b)

结果：
[[6 7 0 5 3]
 [9 5 8 5 0]
 [9 7 6 1 1]
 [7 5 9 8 4]]
 
[[0 5 4 8]
 [4 5 9 1]
 [8 3 9 9]
 [6 2 4 6]
 [0 3 6 9]]
 
[[ 58  84 125 112]
 [114 104 173 179]
 [ 82 103 163 148]
 [140 115 210 226]]
```
```python
a = np.random.randint(10, size=20).reshape(4, 5)
print(a)
print(np.unique(a))
print(sum(a))  #求和，列的和
print(sum(a[0]))  #第一行的和
print(sum(a[:, 0]))  #第一列的和

print(a.max())   #求最大值
print(max(a[0]))   #求第一行最大值
print(max(a[:, 0]))   #求第一列最大值

结果：
[[9 5 9 8 4]
 [0 7 3 8 5]
 [5 2 8 9 6]
 [9 5 0 5 1]]
 
[0 1 2 3 4 5 6 7 8 9]

[23 19 20 30 16]

35

23

9
9
9
```
### Array 的 input 和 output
#### 使用 pickle 序列化 numpy array
```python
import pickle
x = np.arange(10)   #创建一维数组
print(x)
f = open('x.pkl', 'wb')
pickle.dump(x, f)  #将文件存到电脑中

f = open('x.pkl', 'rb')
print(pickle.load(f))
np.save('one_array', x)
print(np.load('one_array.npy'))

y = np.arange(20)
print(y)
np.savez('two_array.npz', a=x, b=y )   #压缩多个文件
c = np.load('two_array.npz')  #加载多个文件并赋值
print(c['a'])
print(c['b'])
```
