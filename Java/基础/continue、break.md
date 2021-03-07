Java：循环控制（continue/break）

break：跳出循环；continue：一次循环到此结束开始下一轮循环

注意：只能对它所在那层循环做

若想一次跳出多层循环，可在循环前放一个标号来标识循环：

**label**：

用带标号的break和continue对那个循环起作用

```java
public class Cash2{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        int amount;
        do{
            System.out.println("请输入金额（1-100）：");
            amount = in.nextInt();
        }while(amount<1 || amount>100);
        Outer://标识整个循环
        for(int one=0;one<=amount;++one)
            for(int five=0;five<=amount/5;++five)
                for(int ten=0;ten<=amount/10;++ten)
                    if(one+five*5+ten*10 == amount){
                        System.out.println（one+"张一元，"+five+"张5元,"+ten+"张10元->"+amount);
                        break Outer;//跳出整个循环
                    }
    }
}
```

