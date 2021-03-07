**注意：**每个数组有一个内部成员length，它会告诉你元素的数量。因此遍历整个数组：

```java
for(int i=0; i<(数组名).length; i++)//不用计数，直接遍历整个数组，i可以记住元素位置
```

for-each循环：for(<类型><变量>：<数组>){}。因此遍历整个数组：

```java
for(int i : numbers)//对于数组numbers中的每一个元素，循环的每一轮把它拿出来作为i，不能记元素位置
{
    System.out.println(numbers[i]);
}
```



```java
package array;

import java.util.Scanner;

public class Array{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        int x;
        double sum = 0;
        int cnt = 0;
        int[] numbers = new int[100];//定义数组，命名：numbers
        x = in.nextInt();
        while(cnt != -1)
        {
            numbers[cnt] = x;//对数组中的元素赋值
            sum += x;
            cnt++;
            x = in.nextInt();
        }
        if(cnt > 0)
        {
            double average = sum/cnt;
            for(int i=0; i<numbers.length; i++)//遍历数组
            {
                if(numbers[i] > average)//使用数组中的元素
                {
                    System.out.println(numbers[i]);//输出数组中的元素
                }
            }
        }
    }
}
```

