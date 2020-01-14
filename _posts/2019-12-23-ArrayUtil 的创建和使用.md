---
title:  ArrayUtil 的创建和使用
date:   2019-12-23 12:00:00
tag:    java
---

### ArrayUtil 的创建和使用

***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！

<head><link rel="stylesheet" href="../css/rouge.css"></head>


ArrayUtil 的创建和使用

代码一：
```java
package five.object;

public class ArrayUtil {
    //求数组的最大值
    public int getMax(int[] arr){
        int max = arr[0];
        for(int i = 1;i < arr.length;i++){
            if(max < arr[i]){
                max = arr[i];
            }
        }
        return max;
    }
    //求数组的最小值
    public int getMin(int[] arr){
        int min = arr[0];
        for(int i = 1;i < arr.length;i++){
            if(min > arr[i]){
                min = arr[i];
            }
        }
        return min;
    }

    //遍历数组元素
    public void printArray(int[] arr){
        System.out.print("[");
        for(int i = 0;i < arr.length;i++){
            System.out.print(arr[i] + "\t");
        }
        System.out.println("]");
    }

    //求数组的平均值
    public int avg(int[] arr){
        int sum = getSum(arr);
        return sum / arr.length;
    }

    //求数组的总和
    public int getSum(int[] arr){
        int sum = 0;
        for(int i = 0;i < arr.length;i++){
            sum += arr[i];
        }
        return sum;
    }

    //数组的反转
    public int[] reverse(int[] arr){
        for(int x = 0,y = arr.length - 1;x < y;x++,y--){
            int temp = arr[x];
            arr[x] = arr[y];
            arr[y] = temp;
        }
        return arr;
    }

    //实现数组的复制
    public int[] copy(int[] arr){
        int[] arr1 = new int[arr.length];
        for(int i = 0;i < arr.length;i++){
            arr1[i] = arr[i];
        }
        return arr1;
    }

    //对数组进行排序
    public void sort(int[] arr,String desc){
        if(desc == "asc") {//ascend :从小到大
            for (int i = 0; i < arr.length - 1; i++) {
                for (int j = 0; j < arr.length - 1 - i; j++) {
                    if (arr[j] > arr[j + 1]) {
//                        int temp = arr[j];
//                        arr[j] = arr[j + 1];
//                        arr[j + 1] = temp;
                        swap(arr,j,j+1);
                    }
                }
            }
        }else if(desc == "desc"){//从大到小
            for (int i = 0; i < arr.length - 1; i++) {
                for (int j = 0; j < arr.length - 1 - i; j++) {
                    if (arr[j] < arr[j + 1]) {
                        swap(arr,j,j+1);
                    }
                }
            }
        }else {
            System.out.println("你输入的排序方式有误！");
        }
    }
    //交换数组中指定位置的元素：交换arr数组中索引为i和j 的两个元素
    public void swap(int[] arr,int i,int j){
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```
代码二：
```java
package five.object;

public class FiveDemoArrayUtil {
    public static void main(String[] args) {
        int[] arr = new int[]{99,66,88,55,-2019,0,2020};

        ArrayUtil au = new ArrayUtil();
        int max = au.getMax(arr);
        System.out.println("最大值为：" + max);

        int avg = au.avg(arr);
        System.out.println("平均值为：" + avg);

        au.printArray(arr);

        System.out.println("反转数组：");
        au.reverse(arr);

        au.printArray(arr);

        System.out.println("对数组排序：");
        au.sort(arr,"desc");//asc

        au.printArray(arr);
    }
}
```