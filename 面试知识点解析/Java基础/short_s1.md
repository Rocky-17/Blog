[参考学习原文链接](https://blog.csdn.net/hurryjiang/article/details/9256959)

```
public class test {
    public static void main(String[] args) {
        short s1 = 1;
        //s1 = s1 + 1;   报错：不兼容的类型: 从int转换到short可能会有损失
        s1 += 1;
        System.out.println(s1);
    }
}
```


```
s1 = s1 + 1;
```
&emsp;&emsp;s1 + 1在进行计算的时候，s1会自动转为int类型，自然s1 + 1也为int类型，将其赋值给short类型的s1就会出现精度损失。  

```
s1 += 1;
```
>Java语言规范中讲到，复合赋值（E1 op=E2）等价于简单赋值（E1=(T)((E1) op (E2))），其中T是E1的类型，除非E1只被计算一次。
>换句话说，复合赋值表达式自动地将所执行计算的结果转型为其左侧变量的类型。如果结果的类型与该变量的类型相同，那么这个转型不会造成任何影响。然而，如果结果的类型比该变量的类型要宽，那么复合赋值操作符将悄悄地执行一个窄化原生类型转换。  