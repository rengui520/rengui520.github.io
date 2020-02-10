---
title:  创建Java类并实例化对象_详解Java类的属性与局部变量_详解Java类的方法的使用
date:   2020-01-14 12:00:00
tag:    java
---

### 创建Java类并实例化对象_详解Java类的属性与局部变量_详解Java类的方法的使用

创建Java类并实例化对象
详解Java类的属性与局部变量
详解Java类的方法的使用

```java
package five.object;
/*
1.面向对象的编程关注于类的设计
2.设计类实际上就是设计类的成员
3.基本的类的成员：属性（成员变量 或 Field） & 方法（函数 或 Method）
 */
/*
一、面向对象思想的落地法则一：
1.设计类，并设计类的成员（成员变量&成员方法）
2.通过类，来创建类的对象（也称作类的实例化）
3.通过:"对象.属性"或"对象.方法" 来调用，完成相应的功能

二、创建的多个对象，彼此各自拥有一套类的属性。当对其中一个对象的属性进行修改时，不会影响到其他对象的属性值。

 三、类的属性（成员变量）
    成员变量 VS 局部变量
    相同点：1.遵循变量声明的格式：数据类型 变量名 = 初始化值;
          2.都有作用域//出了范围不管用
    不同点：1.声明的位置不同：成员变量：声明在类里，方法外
                         局部变量：声明在方法内，方法的形参部分，代码块内
          2.成员变量的修饰符有四个：public private protected 缺省
             局部变量没有修饰符，与所在的方法修饰符相同。
          3.初始化值：一定会有初始化值。
            成员变量：如果在声明的时候，不显式的赋值，那么不同数据类型会有不同的默认初始化值。
                byte short int long ==> 0
                float double ==> 0.0
                char ==> 空格
                boolean ==> false
                引用类型变量 ==> null
            局部变量：一定要显式赋值。（局部变量没有默认初始化值）
          4.二者在内存中存放的位置不同：成员变量存在于堆空间中；局部变量存在于栈空间中。

总结：关于变量的分类:1)按照数据类型分：基本数据类型（8种） & 引用数据类型
                 2）按照声明的位置分：成员变量 & 局部变量


四、类的方法：提供某种功能的实现
    1）实例：public void eat(){//方法体}
            public String getName(){}
            public void setName(String n){}
      格式：权限修饰符 返回值类型（void：无返回值 / 具体的返回值） 方法名(形参){}

    2）关于返回值类型：void:表明此方法不需要返回值
                    有返回值的方法：在方法的最后一定有 return + 返回值类型对应的变量
       记忆：void 与 return 不可以同时出现在一个方法内。
    3）方法内可以调用本类的其他方法或属性，但是不能在方法内再定义方法！
 */

import java.util.Scanner;

public class Five {
    public static void main(String[] args) {
        //基本数据类型的声明：数据类型 变量名 = 初始化值;
        int i = 10;
        //类的实例化：如下的a1就是一个实实在在的对象
        People a1 = new People();//引用数据类型

        //通过对象调用属性
        a1.name = "唐雅";//根据创建的数据类型赋予不同的值。引用数据类型
        a1.age = 22; //int型
        System.out.println("name:" + a1.name + " age:" + a1.age);

        //通过对象调用方法
        a1.eat();
        a1.sleep();

        //再创建一个类的对象
        People a2 = new People();
        System.out.println("name:" + a2.name + " age:" + a2.age);
        a2.name = "唐舞桐";
        a2.age = 14;
        System.out.println("name:" + a2.name + " age:" + a2.age);

        //a3不意为着相较于a1重新创建的一个对象，而是a1与a3共用一个对象实体。
        People a3 = a1;
        System.out.println("name:" + a3.name + " age:" + a3.age);//与 a1 一样
        a3.name = "宁荣荣";
        System.out.println("a1.name:" + a1.name + " age:" + a1.age);

        //讲解二
        System.out.println();
        SevenShrekMonsters s1 = new SevenShrekMonsters();
        s1.info();

        s1.name = "朱竹青";
        s1.age = 18;
        s1.sex = true;
        s1.info();

        s1.setName("江楠楠");//调用方法。与调用属性 s1.name = "江楠楠";的结果一样，
        s1.info();

        System.out.println();
        SevenShrekMonsters s2 = s1;
        System.out.println("s1:" + s1);
        System.out.println("s2:" + s2);
        s2.info();

        System.out.println();
        s2 = new SevenShrekMonsters();
        System.out.println("s2:" + s2);
        s2.info();

        //实例化Scanner类的对象，通过此对象 .nextXxx() 调用。完成相应的功能。
        Scanner s = new Scanner(System.in);
        int a = s.nextInt();

    }
}

//类：是抽象的
class People{
    //1.属性：
    String name;
    int age;
    boolean sex;

    //2.方法
    public void eat(){
        System.out.println("人吃饭");
    }
    public void sleep(){
        System.out.println("人睡觉");
    }
}


class SevenShrekMonsters{
    //1.属性：
    String name;
    int age;
    boolean sex;

    //2.方法
    public void eat(){
        System.out.println("戴雨浩吃饭");
    }
    public void sleep(){
        System.out.println("王冬睡觉");
    }

    //当通过对象调用此方法时，会将方法的方法的返回值提供给方法的调用者，也就是当前的对象
    public String getName(){ //获取名字
        return name;
        //其后不可声明语句
    }
    //给属性name赋值
    public void setName(String n){ //改名
        name = n;
    }
    public void info(){
        //可以方法内可以调用本类的其他方法或属性，但是不能在方法内再定义新的方法！
        eat();
        sleep();
        System.out.println("name:" + name + " age:" + age + " sex:" + sex);

//        //非法
//        public void breath(){
//            System.out.println("决斗啊");
//        }
    }
}
```