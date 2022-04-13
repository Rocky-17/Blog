# POJO(Plain Old Java Object)  

&emsp;&emsp;POJO 是一个普通的 Java 对象，不受任何特殊限制(除了 Java 语言规范所强制的限制之外)的约束，也不需要任何类路径。POJO 用于增加程序的可读性和可重用性。  

## BO(Business Object)  
&emsp;&emsp;业务对象，可以由 Service 层输出的封装业务逻辑的对象。  

## DO(Data Object)  
&emsp;&emsp;此对象与数据库表结构一一对应，通过 DAO 层向上传输数据源对象。

## DTO(Data Transfer Object)  
&emsp;&emsp;数据传输对象，Service 或 Manager 向外传输的对象。

## VO(View Object)  
&emsp;&emsp;显示层对象，通常是 Web 向模板渲染引擎层传输的对象。