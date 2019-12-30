title:  模板方法设计模式(TemplateMethod) 
date:   2019-12-30 12:00:00
tag:    java
---
### 模板方法设计模式(TemplateMethod) 

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

<head><link rel="stylesheet" href="../css/rouge.css"></head>

- 抽象类体现的就是一种模板模式的设计，抽象类作为多个子类的通用模板，子类在抽象类的基础上进行扩展、改造，但子类总体上会保留抽象类的行为方式。
- 解决的问题：
    - 当功能内部一部分实现是确定，一部分实现是不确定的。这时可以把不确定的部分暴露出去，让子类去实现。
    - 编写一个抽象父类，父类提供了多个子类的通用方法，并把一个或多个方法留给其子类实现，就是一种模板模式。

练习：计算时间
```java
package ten;

//模板方法设计模式
public class TestTemplate {
	public static void main(String[] args) {
		new SubTemplate().spendTime();
	}
}

abstract class Template {

	public abstract void code();

	public void spendTime() {
		long start = System.currentTimeMillis();

		this.code();

		long end = System.currentTimeMillis();
		System.out.println("花费的时间为：" + (end - start));
	}
}

class SubTemplate extends Template {
	
	public void code() {
		boolean flag = false;
		for(int i = 2;i <= 10000;i++){
			for(int j = 2;j <= Math.sqrt(i);j++){
				if(i % j == 0){
					flag = true;
					break;
				}
			}
			if(!flag){
				System.out.println(i);
			}
			flag = false;
		}
	}
}
```

