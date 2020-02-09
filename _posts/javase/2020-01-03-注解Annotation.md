---
title:  注解Annotation
date:   2020-01-03 12:00:00
tag:    java
---

### 注解Annotation

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

<head><link rel="stylesheet" href="../css/rouge.css"></head>



主要内容
一、JDK内置的基本注解类型（3个）
注解 (Annotation) 概述：
1. 从 JDK 5.0 开始, Java 增加了对元数据(MetaData) 的支持, 也就是 Annotation(注解)
2. Annotation 其实就是代码里的`特殊标记`, 这些标记可以在编译, 类加载, 运行时被读取, 并执行相应的处理. 通过使用 Annotation, 程序员可以在不改变原有逻辑的情况下, 在源文件中嵌入一些补充信息.
3. Annotation 可以像修饰符一样被使用, 可用于`修饰包,类, 构造器, 方法, 成员变量, 参数, 局部变量的声明`, 这些信息被保存在 Annotation 的 “name=value” 对中.
4. Annotation 能被用来为程序元素(类, 方法, 成员变量等) 设置元数据

基本的 Annotation：
- 使用 Annotation 时要在其前面增加 @ 符号, 并`把该 Annotation 当成一个修饰符使用`。用于修饰它支持的程序元素
- 三个基本的 Annotation:
    - `@Override`: 限定重写父类方法, 该注释只能用于方法
    - `@Deprecated`: 用于表示某个程序元素(类, 方法等)已过时
    - `@SuppressWarnings`: 抑制编译器警告


二、自定义注解类型
三、对注解进行注解（4个）
- `@Retention`: 只能用于修饰一个 Annotation 定义, 用于指定该 Annotation 可以保留多长时间, @Rentention 包含一个 RetentionPolicy 类型的成员变量, 使用 @Rentention 时必须为该 value 成员变量指定值:

    - RetentionPolicy.SOURCE: 编译器直接丢弃这种策略的注释
    - RetentionPolicy.CLASS: 编译器将把注释记录在 class 文件中. 当运行 Java 程序时, JVM 不会保留注解。 这是默认值
    - RetentionPolicy.RUNTIME:编译器将把注释记录在 class 文件中. 当运行 Java 程序时, JVM 会保留注释. 程序可以通过反射获取该注释

- `@Target`: 用于修饰 Annotation 定义, 用于指定被修饰的 Annotation 能用于修饰哪些程序元素. @Target 也包含一个名为 value 的成员变量.
- @Documented: 用于指定被该元 Annotation 修饰的 Annotation 类将被 javadoc 工具提取成文档.
    - 定义为Documented的注解必须设置Retention值为RUNTIME。
- @Inherited: 被它修饰的 Annotation 将具有`继承性`.如果某个类使用了被 @Inherited 修饰的 Annotation, 则其子类将自动具有该注解
    - 实际应用中，使用较少


四、利用反射获取注解信息（在反射部分涉及）


代码一：
```java
package fourteen;

import java.util.ArrayList;
import java.util.List;

/*
 * 注解
 * 1.JDK提供的常用的注解
 *  @Override: 限定重写父类方法, 该注释只能用于方法
	@Deprecated: 用于表示某个程序元素(类, 方法等)已过时
	@SuppressWarnings: 抑制编译器警告
   2.如何自定义一个注解
   3.元注解

 */
public class TestAnnotation {
	public static void main(String[] args) {
		Person p = new Student1();
		p.walk();
		p.eat();
		
		@SuppressWarnings({ "rawtypes", "unused" })
		List list = new ArrayList();
		
		@SuppressWarnings("unused")
		int i = 10;
//		System.out.println(i);
	}
}
@MyAnnotation(value = "atguigu")
class Student1 extends Person{
	//表明重写父类
	@Override
	public void walk(){
		System.out.println("学生走路");
	}
	@Override
	public void eat(){
		System.out.println("学生吃饭");
	}
}
@Deprecated
class Person{
	String name;
	int age;
	
	public Person() {
		super();
	}
	@MyAnnotation(value = "atguigu")
	public Person(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}
	@MyAnnotation(value = "atguigu")
	public void walk(){
		System.out.println("走路");
	}
	@Deprecated
	public void eat(){
		System.out.println("吃饭");
	}
	@Override
	public String toString() {
		return "Person [name=" + name + ", age=" + age + "]";
	}
	
}
```

代码二：
```java
package fourteen;

import static java.lang.annotation.ElementType.CONSTRUCTOR;
import static java.lang.annotation.ElementType.FIELD;
import static java.lang.annotation.ElementType.LOCAL_VARIABLE;
import static java.lang.annotation.ElementType.METHOD;
import static java.lang.annotation.ElementType.PARAMETER;
import static java.lang.annotation.ElementType.TYPE;

import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

//自定义的注解
@Target({TYPE,FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
	String value() default "hello";
}
```