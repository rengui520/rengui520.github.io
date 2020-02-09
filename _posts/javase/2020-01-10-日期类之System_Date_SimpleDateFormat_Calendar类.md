---
title:  日期类之System_Date_SimpleDateFormat_Calendar类
date:   2020-01-10 12:00:00
tag:    java
---

### 日期类之System_Date_SimpleDateFormat_Calendar类

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

<head><link rel="stylesheet" href="../css/rouge.css"></head>


日期类    
1.java.lang.System类    

System类提供的public static long currentTimeMillis()用来返回当前时间与1970年1月1日0时0分0秒之间以毫秒为单位的时间差。   
    > 此方法适于计算时间差。

计算世界时间的主要标准有：   
UTC(Universal Time Coordinated)    
GMT(Greenwich Mean Time)    
CST(Central Standard Time)   


2. java.util.Date 类
    表示特定的瞬间，精确到毫秒

- 构造方法：
    - `Date( )`使用Date类的无参数构造方法创建的对象可以获取本地当前时间。
    - `Date(long date)`
- 常用方法
    - `getTime()`:返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。
    - `toString()`:把此 Date 对象转换为以下形式的 String： dow mon dd hh:mm:ss zzz yyyy 其中： dow 是一周中的某一天 (Sun, Mon, Tue, Wed, Thu, Fri, Sat)，zzz是时间标准。


Date 类的API不易于国际化，大部分被废弃了，`java.text.Simp
leDateFormat` 类是一个不与语言环境有关的方式来格式化和解析日期的具体类。

- 它允许进行格式化（日期文本）、解析（文本日期）
- 格式化：
    - `SimpleDateFormat()` ：默认的模式和语言环境创建对象
    - `public SimpleDateFormat(String pattern)`：该构造方法可以用参数pattern指定的格式创建一个对象，该对象调用：
    - `public String format(Date date)`：方法格式化时间对象date
- 解析：
    - `public Date parse(String source)`：从给定字符串的开始解析文本，以生成一个日期。

3. `java.util.Calendar(日历)类`
     Calendar是一个抽象基类，主用用于完成日期字段之间相互操作的功能。
- 获取Calendar实例的方法
    - 使用 `Calendar.getInstance()` 方法
    - 调用它的子类 `GregorianCalendar` 的构造器。

- 一个Calendar的实例是系统时间的抽象表示，通过 `get(int field)` 方法来取得想要的时间信息。比如YEAR、MONTH、DAY_OF_WEEK、HOUR_OF_DAY 、MINUTE、SECOND
    - `public void set(int field,int value)`
    - `public void add(int field,int amount)`
    - `public final Date getTime()`
    - `public final void setTime(Date date)`


```java
package eighteen;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

import org.junit.Test;

/*
 * 与时间相关的类：
 * 1.System 类下的currentTimeMillis();
 * 2.Date类:java.util.Date 
 *    如何创建其实例；其下的方法：toString()、getTime()
 *    (以及其子类java.sql.Date)
 * 3.SimpleDateFormat类
 * 4.Calendar类
 */
public class TestDate {
	
	
	//日历：Calendar类   get()/add()/set()/Date getTime()/setTime(Date d)
	@Test
	public void test4(){
		Calendar c = Calendar.getInstance();
		int day = c.get(Calendar.DAY_OF_MONTH);//获取当天是当月的第几天
		System.out.println(day);
		
		c.add(Calendar.DAY_OF_MONTH, -2);//在第几天上进行加减操作
		day = c.get(Calendar.DAY_OF_MONTH);
		System.out.println(day);
		
		c.set(Calendar.DAY_OF_MONTH, 23);
		Date d = c.getTime();
		System.out.println(d);
		
	}
	
	
	/*
	 * “三天打渔两天晒网”  1990-01-01  XXXX-XX-XX 打渔？晒网？
	 */
	//返回date1与date2之间的天数,date1早于date2
	public int getDays(String date1,String date2) throws ParseException {
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
		Date d1 = sdf.parse(date1);
		Date d2 = sdf.parse(date2);
		long milliTime = d2.getTime()-d1.getTime();
		return (int)milliTime/1000/3600/24 + 1;
	}
	
	@Test
	public void test3() throws ParseException{
		String str1 = "1990-01-01";
		String str2 = "1990-01-06";
		int dates = getDays(str1,str2);
		
		if(dates % 5 == 0 || dates % 5 == 4){
			System.out.println("晒网");
		}else{
			System.out.println("打渔");
		}
	}
	
	/*
	 * java.text.SimpleDateFormat类易于国际化
	 * 格式化：日期--->文本 使用SimpleDateFormat的format()方法
	 * 解析：文本--->日期 使用SimpleDateFormat的parse()方法
	 */
	@Test
	public void test2() throws Exception{
		//1.格式化1
		SimpleDateFormat sdf = new SimpleDateFormat();
		String date = sdf.format(new Date());
		System.out.println(date);//20-1-11 下午3:20
		//2.格式化2
		SimpleDateFormat sdf1 = new SimpleDateFormat("EEE, d MMM yyyy HH:mm:ss Z");
		date = sdf1.format(new Date());
		System.out.println(date);//星期六, 11 一月 2020 15:20:36 +0800
		
		//3.解析：
		Date date1 = sdf.parse("20-1-11 下午3:20");
		System.out.println(date1);
		
		date1 = sdf1.parse("星期六, 11 一月 2020 15:20:36 +0800");
//		date1 = sdf1.parse("20-1-11 下午3:20");//格式不对
		System.out.println(date1);
	}
	//java.util.Date不易于国际化
	@Test
	public void test1(){
//		java.sql.Date d3 = new java.sql.Date(1578716715730L);
//		System.out.println(d3);//2456-03-08
		//创建一个Date的实例
		Date d1 = new Date();
		System.out.println(d1.toString());// Sat Jan 11 12:25:15 CST 2020
		System.out.println(d1.getTime());//返回时间的 long 型的值 1578716715730
		Date d2 = new Date(1578716715730L);
		System.out.println(d2);
	}
}	
```