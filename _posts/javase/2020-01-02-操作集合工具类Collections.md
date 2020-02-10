---
title:  操作集合工具类：Collections
date:   2020-01-02 12:00:00
tag:    java
---
###  操作集合工具类：Collections



- Collections 是一个操作 Set、List 和 Map 等集合的工具类
- Collections 中提供了一系列静态的方法对集合元素进行排序、查询和修改等操作，还提供了对集合对象设置不可变、对集合对象实现同步控制等方法
- 排序操作：（均为static方法）
    - reverse(List)：反转 List 中元素的顺序
    - shuffle(List)：对 List 集合元素进行随机排序
    - sort(List)：根据元素的自然顺序对指定 List 集合元素按升序排序
    sort(List，Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序
    - swap(List，int， int)：将指定 list 集合中的 i 处元素和 j 处元素进行交换

- 查找、替换
    - Object max(Collection)：根据元素的自然顺序，返回给定集合中的最大元素
    - Object max(Collection，Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素
    - Object min(Collection)
    - Object min(Collection，Comparator)
    - int frequency(Collection，Object)：返回指定集合中指定元素的出现次数
    - void copy(List dest,List src)：将src中的内容复制到dest中
    - boolean replaceAll(List list，Object oldVal，Object newVal)：使用新值替换 List 对象的所有旧值

- 同步控制
    - Collections 类中提供了多个 synchronizedXxx() 方法，该方法可使将指定集合包装成线程同步的集合，从而可以解决多线程并发访问集合时的线程安全问题


```java
package thirteen;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

import org.junit.Test;

/*
 * 操作 Collection 以及 Map 的工具类：Collections
 * 
 * 面试题：区分 Collection 与 Collections
 * 
 */
public class TestCollections {
	/*
	 *  Object max(Collection)：根据元素的自然顺序，返回给定集合中的最大元素
		Object max(Collection，Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素
		Object min(Collection)
		Object min(Collection，Comparator)
		int frequency(Collection,Object)：返回指定集合中指定元素的出现次数
		void copy(List dest,List src)：将src中的内容复制到dest中
		boolean replaceAll(List list，Object oldVal，Object newVal)：使用新值替换 List 对象的所有旧值

	 */
	@Test
	public void testCollections2(){
		List list = new ArrayList();
		list.add(123);
		list.add(456);
		list.add(12);
		list.add(78);
		list.add(456);
		Object obj = Collections.max(list);
		System.out.println(obj);
		int count = Collections.frequency(list, 4567);
		System.out.println(count);
		//实现List的复制
		//List list1 = new ArrayList();//错误的实现方式
		List list1 = Arrays.asList(new Object[list.size()]);
		Collections.copy(list1, list);
		System.out.println(list1);
		//通过如下的方法保证list的线程安全性。
		List list2 = Collections.synchronizedList(list);
		System.out.println(list2);
	}
	/*
	 *  reverse(List)：反转 List 中元素的顺序
		shuffle(List)：对 List 集合元素进行随机排序
		sort(List)：根据元素的自然顺序对指定 List 集合元素按升序排序
		sort(List，Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序
		swap(List，int， int)：将指定 list 集合中的 i 处元素和 j 处元素进行交换
		
	 */
	@Test
	public void testCollections1(){
		List list = new ArrayList();
		list.add(123);
		list.add(456);
		list.add(12);
		list.add(78);
		System.out.println(list);
		Collections.reverse(list);
		System.out.println(list);
		Collections.shuffle(list);
		System.out.println(list);
		Collections.sort(list);
		System.out.println(list);
		Collections.swap(list, 0, 2);
		System.out.println(list);
	}
}
```