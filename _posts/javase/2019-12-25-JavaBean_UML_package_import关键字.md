---
title:  JavaBean_UML_package_import关键字
date:   2019-12-25 12:00:00
tag:    java
---

### JavaBean_UML_package_import关键字

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

<head><link rel="stylesheet" href="../css/rouge.css"></head>

```java
package seven;

/**
 * package:声明源文件所在的包，写在程序的第一行
 *  每「.」一次，表示一层文件目录
 *  包名都要小写
 *
 * import:
 *  1）显式的导入指定包下的类或接口
 *  2）写在包名和源文件之间
 *  3）如果需要引入多个类或接口，那么就并列写出
 *  4）如果导入的类是 Java.lang 包下的，如：System String  Math 等，就不需要显式的声明。
 *  5） 理解「.*」的概念。表示所有的。
 *  6）如何处理同名类的导入。如：在 util 包和 sql 包下同时存在 Date 类。
 *  7）import static 表示导入指定类的 static 的属性或方法。
 *  8）导入「java.lang.*」只能导入lang 包下的所有类和接口，不能导入lang的子包下的类或接口。
 *
 */
/**
 * 1.java.lang：包含一些Java语言的核心类，如String、Math、Integer、System和Thread，提供常用功能。
 * 2.java.net：包含执行与网络相关的操作的类和接口。
 * 3.java.io：包含能提供多种输入/输出功能的类。
 * 4.java.util：包含一些实用工具类，如定义系统特性、接口的集合框架类、使用与日期日历相关的函数。
 * 5.java.text：包含了一些java格式化相关的类
 * 6.java.sql：包含了java进行JDBC数据库编程的相关类/接口
 * 7.java.awt：包含了构成抽象窗口工具集（abstract window toolkits）的多个类，
 *   这些类被用来构建和管理应用程序的图形用户界面(GUI)。
 * 8.java.applet：包含applet运行所需的一些类。
 */
//import java.util.Scanner;
//import java.util.Date;
//import java.util.List;
//import java.util.ArrayList;
import java.util.*;
import static java.lang.System.*;
public class TestPackageImport {
    public static void main(String[] args) {
        out.println("Hello World");
        Scanner s = new Scanner(System.in);
        s.next();

        Date d = new Date();
        List list = new ArrayList();

        java.sql.Date d1 = new java.sql.Date(2553434L);
    }
}

```