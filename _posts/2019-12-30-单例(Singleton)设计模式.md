---              
title:  单例 (Singleton)设计模式
date:   2019-12-30 12:00:00
tag:    java
---
### 单例 (Singleton)设计模式

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

<head><link rel="stylesheet" href="../css/rouge.css"></head>

一、 单例 (Singleton)设计模式

设计模式是在大量的实践中总结和理论化之后优选的代码结构、编程风格、以及`解决问题的思考方`式。设计模式就像是经典的棋谱，不同的棋局，我们用不同的棋谱，免去我们自己再思考和摸索。
        
        
所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类只能存在一个对象实例，并且`该类只提供一个取得其对象实例的方法`。如果我们要让类在一个虚拟机中只能产生一个对象，我们首先必须将类的`构造方法的访问权限设置为private`，这样，就不能用new操作符在类的外部产生类的对象了，但在类内部仍可以产生该类的对象。因为在类的外部开始还无法得到类的对象，只能`调用该类的某个静态方法`以返回类内部创建的对象，静态方法只能访问类中的静态成员变量，所以，指向类内部产生的该`类对象的变量也必须定义成静态的`。


二、设计模式及单例模式的饿汉式实现
```java
package nine;

/*
 * 设计模式：设计模式是在大量的实践中总结和理论化之后优选的代码结构、编程风格、以及解决问题的思考方式。
 * 23种设计模式。
 *
 * 单例的设计模式：
 * 1.解决的问题：使得一个类只能够创建一个对象。
 * 2.如何实现？见如下的4步
 */
//饿汉式
public class TestSingleton {
	public static void main(String[] args) {
		Singleton s1 = Singleton.getInstance();
		Singleton s2 = Singleton.getInstance();
		System.out.println(s1 == s2);
	}
}
//只能创建Singleton的单个实例
class Singleton{

	//1.私有化构造器，使得在类的外部不能够调用此构造器
	private Singleton(){

	}
	//2.在类的内部创建一个类的实例
	private static Singleton instance = new Singleton();
	//3.私有化此对象，通过公共的方法来调用
	//4.此公共的方法，只能通过类来调用，因为设置为static的,同时类的实例也必须为static声明的
	public static Singleton getInstance(){
		return instance;
	}

}
```

三、设计模式及单例模式的懒汉式实现
```java
package nine;

//懒汉式:可能存在线程安全问题的
public class TestSingleton1 {
	public static void main(String[] args) {
		Singleton1 s1 = Singleton1.getInstance();
		Singleton1 s2 = Singleton1.getInstance();
		System.out.println(s1 == s2);

	}
}
class Singleton1{
	//1.
	private Singleton1(){

	}
	//2.
	private static Singleton1 instance = null;
	//3.
	public static Singleton1 getInstance(){
		if(instance == null){
			instance = new Singleton1();
		}
		//自我总结：第一次时，因初始值为null，故生成一个对象，且返回该对象。第二次时，条件不满足，故返回上一次的对象。
		return instance;
	}
}
```