---
title:  RandomAccessFile 类使用
date:   2020-01-04 12:00:00
tag:    java
---

### RandomAccessFile 类的使用

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

<head><link rel="stylesheet" href="../css/rouge.css"></head>


- RandomAccessFile 类支持 “随机访问” 的方式，程序可以直接跳到文件的任意地方来读、写文件
    - 支持只访问文件的部分内容
    - 可以向已存在的文件后追加内容
- RandomAccessFile 对象包含一个记录指针，用以标示当前读写处的位置。RandomAccessFile 类对象可以自由移动记录指针：
    - `long getFilePointer()`：获取文件记录指针的当前位置
    - `void seek(long pos)`：将文件记录指针定位到 pos 位置

- 构造器
    - public RandomAccessFile(File file, String mode) 
    - public RandomAccessFile(String name, String mode)
 
- 创建 RandomAccessFile 类实例需要指定一个 mode 参数，该参数指定 RandomAccessFile 的访问模式：
    - `r: 以只读方式打开`
    - `rw：打开以便读取和写入`
    - `rwd:打开以便读取和写入；同步文件内容的更新`
    - `rws:打开以便读取和写入；同步文件内容和元数据的更新`


```java
package fifteen;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.RandomAccessFile;

import org.junit.Test;

/*
 * RandomAccessFile:支持随机访问
 * 1.既可以充当一个输入流，有可以充当一个输出流
 * 2.支持从文件的开头读取、写入
 * 3.支持从任意位置的读取、写入（插入）
 */
public class TestRandomAccessFile {
	//相较于test3，更通用，多行的效果
	@Test
	public void test4(){
		RandomAccessFile raf = null;
		try {
			raf = new RandomAccessFile(new File("hello1.txt"),"rw");
			
			raf.seek(4);
			byte[] b = new byte[10];
			int len;
			StringBuffer sb = new StringBuffer();
			while((len = raf.read(b)) != -1){
				sb.append(new String(b,0,len));//读取
			}
			raf.seek(4);
			raf.write("xy".getBytes());
			raf.write(sb.toString().getBytes());//写入
		}catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}finally{
			if(raf != null){
				try {
					raf.close();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
		}
	}
	
	//实现插入的效果：在d字符后面插入“xy”  。单行的效果
	@Test
	public void test3(){
		RandomAccessFile raf = null;
		try {
			raf = new RandomAccessFile(new File("hello1.txt"),"rw");
			
			raf.seek(4);
			String str = raf.readLine();//efg123456
//			long l = raf.getFilePointer();//查看目前指针在哪
//			System.out.println(l);
			
			raf.seek(4);
			raf.write("xy".getBytes());
			raf.write(str.getBytes());
		}catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}finally{
			if(raf != null){
				try {
					raf.close();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				
			}
		}
	}
	
	//实现的实际上是覆盖的效果
	@Test
	public void test2(){
		RandomAccessFile raf = null;
		try {
			raf = new RandomAccessFile(new File("hello1.txt"),"rw");
			
			raf.seek(4);
			raf.write("xy".getBytes());
		}catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}finally{
			if(raf != null){
				try {
					raf.close();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				
			}
		}
	}
	
	//进行文件的读、写
	@Test
	public void test1(){
		RandomAccessFile raf1 = null;
		RandomAccessFile raf2 = null;
		try {
			raf1 = new RandomAccessFile(new File("hello.txt"), "r");
			raf2 = new RandomAccessFile(new File("hello1.txt"),"rw");
			
			byte[] b = new byte[20];
			int len;
			while((len = raf1.read(b)) != -1){
				raf2.write(b, 0, len);
			}
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}finally{
			if(raf2 != null){
				try {
					raf2.close();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
			if(raf1 != null){
				try {
					raf1.close();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				
			}
		}
	}
}
```