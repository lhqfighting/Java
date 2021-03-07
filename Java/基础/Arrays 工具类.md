## Arrays 工具类

##### 主要操作

1. 数组排序
2. 有序数组的二分查找(binarySearch)
3. 转列表(asList)
4. 数组复制(arraycopy)
5. 数组转字符串
6. 数组比较判等
7. 计算数组哈希值
8. 数组填充

##### 常用函数

```java
public class Arrays {
    //默认升序的排序算法
    //串行排序算法，底层实现是双轴快速排序，后两个参数可选
    public static void sort(int[] a, int fromIndex, int toIndex)
    //并行排序算法，底层是归并排序，需要额外空间，后三个参数可选
    public static <T> void parallelSort(T[] a, int fromIndex, int toIndex,
                                        Comparator<? super T> cmp)
/*---------------------------------------------------------------------------*/
    //有序数组的二分查找，范围参数可选
    public static int binarySearch(int[] a, int fromIndex, int toIndex,
                                   int key)
/*---------------------------------------------------------------------------*/
    //可变参数转列表
    public static <T> List<T> asList(T... a)
/*---------------------------------------------------------------------------*/
    //数组拷贝，底层调用System.arraycopy()这个 native 方法
    public static int[] copyOf(int[] original, int newLength)
/*---------------------------------------------------------------------------*/
    //数组内容转字符串
    public static String toString(int[] a)
    //高维数组转字符串，递归转换
    public static String deepToString(Object[] a)
/*---------------------------------------------------------------------------*/
    //数组元素依次比较，判等
    public static boolean equals(int[] a, int[] a2)
    //高维数组判等，递归判断
    public static boolean deepEquals(Object[] a1, Object[] a2)
/*---------------------------------------------------------------------------*/
    //数组对象的 hash 码的计算
    public static int hashCode(int a[])
    //高维数组 hash 码的计算，递归计算
    public static int deepHashCode(Object a[])
/*---------------------------------------------------------------------------*/
    //数组填充指定值，中间两个范围参数可选
    public static void fill(int[] a, int fromIndex, int toIndex, int val)
}
```

#####  二分查找

源码如下：

```java
public static int binarySearch(int[] a, int key) {
    return binarySearch0(a, 0, a.length, key);
}
public static int binarySearch(int[] a, int fromIndex, int toIndex,
                               int key) {
    rangeCheck(a.length, fromIndex, toIndex);
    return binarySearch0(a, fromIndex, toIndex, key);
}

// 二分查找
private static int binarySearch0(int[] a, int fromIndex, int toIndex,
                                 int key) {
    int low = fromIndex;
    int high = toIndex - 1;

    while (low <= high) {
        int mid = (low + high) >>> 1;
        int midVal = a[mid];

        if (midVal < key)
            low = mid + 1;
        else if (midVal > key)
            high = mid - 1;
        else
            return mid; // 找到了 key
    }
    return -(low + 1);  // 没有找到 key
}
```

其实大致上就是常规的二分查找的写法，主要注意没有找到 key 时的返回值，为 `-(low + 1)`。
 其负数表示如果 key 存在，则 key 应该在数组的哪个位置（**从 1 开始**）上。

```java
Integer[] data = {1, 2, 5, 10, 12};\\数组长度为 5 
//输出 -1，如果 -3 存在，数组为{-3, 1, 2, 5, 10, 12 }
//表示 -3 应该在原数组中的第 1 个位置上
System.out.println(Arrays.binarySearch(data,-3));
//输出 -3，如果 3 存在，数组为{1, 2, 3, 5, 10, 12}
//表示 3 应该在原数组中第 3 个位置上
System.out.println(Arrays.binarySearch(data, 3));
//输出 -4，如果 8 存在，数组为{1, 2, 5, 8, 10, 12}
//表示 8 应该在原数组中第 4 个位置上
System.out.println(Arrays.binarySearch(data, 8));
//输出 -6，如果 20 存在，数组为{1, 2, 5, 10, 12, 20}
//表示 20 应该在原数组中第 6 个位置上
System.out.println(Arrays.binarySearch(data, 20));
```

#####  数组复制

源码如下：

```
public static int[] copyOf(int[] original, int newLength) {
    int[] copy = new int[newLength];
    System.arraycopy(original, 0, copy, 0,
                     Math.min(original.length, newLength));
    return copy;
}
```

其底层调用的是 `java.lang` 包下的 `System` 类的 `arraycopy()` 方法，这个方法是一个本地 (native) 方法。源码如下：

```java
public static native void arraycopy(Object src,  int  srcPos,
        Object dest, int destPos,
        int length);
```

##### 数组填充

数组填充其实就是对数组元素进行批量赋值的操作。
 源码如下：

```java
public static void fill(int[] a, int fromIndex, int toIndex, int val) {
    rangeCheck(a.length, fromIndex, toIndex);//判断是否越界
    for (int i = fromIndex; i < toIndex; i++)
        a[i] = val;
}
```

可以看到，和我们自己写代码实现没差别，并没有做什么优化操作。所以需要进行数组填充时，我们可以选择自己实现，也可以选择调用这个方法，效果都一样。

