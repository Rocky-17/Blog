# static  

[参考学习原文连接:深入分析java中的关键字static - 愚公要移山的文章 - 知乎](https://zhuanlan.zhihu.com/p/70110497)

## static修饰类 

&emsp;&emsp;普通类不能使用static来修饰，内部类才可以。  

```
//如果内部类没有static修饰，只能通过外部类实例来创建内部类的实例对象：
public class test {
    public class InnerClass{
        InnerClass(){
            System.out.println("部类");
        }
        public void InnerMethod() {
            System.out.println("内部方法");
        }
    }
    public static void main(String[] args) {
        test nt = new test();
        test.InnerClass inner = nt.new InnerClass();
        inner.InnerMethod();
    }
}
```
```
//内部类有static修饰：
public class test {
    //static关键字修饰内部类
    public static class InnerClass{
        InnerClass(){
            System.out.println("静态内部类");
        }
        public void InnerMethod() {
            System.out.println("静态内部方法");
        }
    }
    public static void main(String[] args) {
        //直接通过test类名访问静态内部类InnerClass
        InnerClass inner=new test.InnerClass();
        //静态内部类可以和普通类一样使用
        inner.InnerMethod();
    }
}
```

## static修饰方法
```
//方法没有static修饰不能直接通过类名调用，需要先创建类的实例。
public class Method {
    public void test() {
        System.out.println("方法");
    };
    public static void main(String[] args) {
        //方式一：直接通过类名
        //Method.test();  //报错：无法从静态上下文中引用非静态方法test()
        //方式二：
        Method method=new Method();
        method.test();
    }
}
```
```
//static修饰方法可以直接通过类名调用方法
public class StaticMethod {
    public static void test() {
        System.out.println("静态方法");
    };
    public static void main(String[] args) {
        StaticMethod.test();
    }
}
```

## static修饰变量  

&emsp;&emsp;static修饰的变量叫做静态变量也叫类变量，属于类，可以直接通过类名调用。没有static修饰的变量叫做实例变量(成员变量），属于实例。
```
public class test {
    static String a = "类变量";
    String b = "实例变量";
    public static void main(String[] args) {
        System.out.println(a);
        System.out.println(test.a);
        //System.out.println(b);  //无法从静态上下文中引用非静态 变量 b
        //System.out.println(test.b);   //无法从静态上下文中引用非静态 变量 b
        test test = new test();
        //System.out.println(b);  //无法从静态上下文中引用非静态变量b
        System.out.println(test.b);
    }
}
```

## 总结：  
&emsp;&emsp;1.静态变量数据存储在方法区（共享数据区）的静态区，所以也叫对象的共享数据。  
&emsp;&emsp;2.静态方法只能访问静态成员。（非静态既可以访问静态，又可以访问非静态）
&emsp;&emsp;3.静态方法中不可以使用this或者super关键字。