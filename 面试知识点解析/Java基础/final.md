# final  

## final修饰类  
&emsp;&emsp;final修饰类表示类不可以被继承
```
public class test {
    final class father{};
    class son extends father{}; //报错：无法从最终test.father进行继承
    public static void main(String[] args) {
    }
}
```  

## final修饰方法  
&emsp;&emsp;fianl修饰的方法不能重写但是能重载。  

## final修饰变量  

```
public class test {
    final static int a = 0; //修饰类变量，需在声明时赋值。
    //final static int b;   报错：变量d未在默认构造器中初始化

    final int c = 0;    //修饰成员变量，需在声明时赋值。
    //final int d;  报错：变量d未在默认构造器中初始化
    public static void main(String[] args) {
        final int e;    //修饰局部变量，声明时可以不赋值。但只能赋值一次。
        e = 0;
        //e = 1;  报错：可能已分配变量e

        // final修饰引用类型变量,可以修改引用对象变量的值，但不可以修改引用对象。(xx号房间住的客人可以改变，xx号对应的房间不能改变)
        int[] temp = {3,2,1};
        final int[] arr = {1,2,3};
        arr[1] = 0;   //合法
        //arr = temp; 报错：无法为最终变量arr分配值
    }
}
```