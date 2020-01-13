---
title:  Math类_BigInteger类_BigDecimal类
date:   2020-01-10 12:00:00
tag:    java
---

### Math 类、BigInteger 类、BigDecimal 类

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

<head><link rel="stylesheet" href="../css/rouge.css"></head>


Math 类
java.lang.Math 提供了一系列静态方法用于科学计算；其方法的参数和返回值类型一般为 double 型。
```
abs     绝对值
acos,asin,atan,cos,sin,tan  三角函数
sqrt     平方根
pow(double a,doble b)     a的b次幂
log    自然对数
exp    e为底指数
max(double a,double b)   求两数较大值
min(double a,double b)   求两数较小值
random()      返回0.0到1.0的随机数
long round(double a)     double型数据a转换为long型（四舍五入）
toDegrees(double angrad)     弧度—>角度
toRadians(double angdeg)     角度—>弧度
```

BigInteger类
Integer类作为int的包装类，能存储的最大整型值为2^31−1，BigInteger类的数字范围较Integer类的数字范围要大得多，可以支持任意精度的整数。
- 构造器
    - BigInteger(String val)
- 常用方法
```
public BigInteger abs()
public BigInteger add(BigInteger val)
public BigInteger subtract(BigInteger val)
public BigInteger multiply(BigInteger val)
public BigInteger divide(BigInteger val)
public BigInteger remainder(BigInteger val)
public BigInteger pow(int exponent)
public BigInteger[] divideAndRemainder(BigInteger val)
```

BigDecimal类
一般的Float类和Double类可以用来做科学计算或工程计算，但在商业计算中，要求数字精度比较高，故用到java.math.BigDecimal类。BigDecimal类支持任何精度的定点数。
- 构造器
    - public BigDecimal(double val)
    - public BigDecimal(String val)
- 常用方法
```
public BigDecimal add(BigDecimal augend)
public BigDecimal subtract(BigDecimal subtrahend)
public BigDecimal multiply(BigDecimal multiplicand)
public BigDecimal divide(BigDecimal divisor, int scale, int roundingMode)
```

```java
package eighteen;

import java.math.BigDecimal;
import java.math.BigInteger;

import org.junit.Test;

public class TestBigDecimal {
	@Test
	public void testBigInteger() {
		BigInteger bi = new BigInteger("12433241123");
		BigDecimal bd = new BigDecimal("12435.351");
		BigDecimal bd2 = new BigDecimal("11");
		System.out.println(bi);
		// System.out.println(bd.divide(bd2));
		System.out.println(bd.divide(bd2, BigDecimal.ROUND_HALF_UP));
		System.out.println(bd.divide(bd2, 15, BigDecimal.ROUND_HALF_UP));
	}

}
```