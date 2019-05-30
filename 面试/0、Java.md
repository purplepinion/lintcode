##### 1.谈谈对Java的理解

> * 平台无关性（一次编译，到处运行）
> * GC
> * 语言特性（泛型、反射，内省，lambda表达式）
> * 面向对象（封装、继承、多态）
> * 类库（集合、并发库、网络库、IO、NIO）
> * 异常处理



##### 2.平台无关性怎么实现

> Java源代码（Java文件）被Java编译器编译，编译成字节码，也就是class文件。Java为不同平台windows、Linux、macOS提供不同的平台虚拟机。class文件在虚拟机运行可以忽略平台特性，将字节码转化成具体平台上的机器指令。
>
> javac	MyClass.java	MyClass.class
>
> java	MyClass	运行
>
> javap -c MyClass	将Java字节码反汇编



##### 3.Java为什么要使用字节码而不是直接编译源文件到机器指令

> 源码编译成字节码分为：词法分析、语法分析、语义分析、中间代码生成、中间代码优化、目标代码
>
> 使用字节码文件可以在每次运行程序时，直接从中间代码开始，跳过之前的阶段，加速编译过程。
>
> 
>
> 同时也可以将其他语言编译成字节码文件让Java虚拟机兼容其他语言。



##### 4.Java虚拟机如何加载class文件 

<https://www.cnblogs.com/Qian123/p/5707562.html>

![1559229378146](C:\Users\chrisz\AppData\Roaming\Typora\typora-user-images\1559229378146.png)

> JVM是对物理计算机的仿真，通过操作系统和计算机硬件交互，JVM 是一个内存中的虚拟机，我们写的所有类、常量、变量、方法都在内存中，JVM具有自己的CPU、寄存器、指令系统等。JVM屏蔽了具体平台的相关信息，使得java程序只需生成Java字节码就可以在多种平台的Java虚拟机上运行。
>
> 
>
> JVM由
>
> * ClassLoader
>
> * Runtime Data Area
>
> * Excution Engine
>
> * Native Interface
>
> 组成。
>
> 
>
> Class Loader 只管加载，只要符合文件结构就加载，至于说能不能运行，则不是它负责的，那是由Execution Engine 负责的。
>
> ---
>
> 1.隐式装载， 程序在运行过程中当碰到通过new 等方式生成对象时，隐式调用类装载器加载对应的类到jvm中。
>
> 2.显式装载， 通过class.forname()等方法，显式加载需要的类 。
>
> 
>
> Java类的加载是动态的，它并不会一次性将所有类全部加载后再运行，而是保证程序运行的基础类(像是基类)完全加载到jvm中，至于其他类，则在需要的时候才加载。这当然就是为了节省内存开销。
>
> 
>
> Java的类加载器有三个，对应Java的三种类:（java中的类大致分为三种：   1.系统类   2.扩展类 3.由程序员自定义的类 ）
>
> ​     Bootstrap Loader  // 负责加载**系统类** (指的是内置类，像是String，对应于C#中的System类和C/C++标准库中的类)
> ​            | 
> ​          \- - ExtClassLoader   // 负责加载**扩展类**(就是继承类和实现类)
> ​                          | 
> ​                      \- - AppClassLoader   // 负责加载应用类(**程序员自定义的类**)
>
> Java采用了委托模型机制。
>
> 委托模型机制的工作原理很简单：当类加载器需要加载类的时候，先请示其Parent(即上一层加载器)在其搜索路径载入，如果找不到，才在自己的搜索路径搜索该类。这样的顺序其实就是加载器层次上自顶而下的搜索，因为加载器必须保证基础类的加载。之所以是这种机制，还有一个安全上的考虑：如果某人将一个恶意的基础类加载到jvm，委托模型机制会搜索其父类加载器，显然是不可能找到的，自然就不会将该类加载进来。
>
> ​      我们可以通过这样的代码来获取类加载器:
>
> ```java
> ClassLoader loader = ClassName.class.getClassLoader();
> ClassLoader ParentLoader = loader.getParent();
> ```
>
> 前面是对类加载器的简单介绍，它的原理机制非常简单，就是下面几个步骤:
>
> 1.装载:查找和导入class文件;
>
> 2.连接:
>
> ​      (1)检查:检查载入的class文件数据的正确性;
>
> ​      (2)准备:为类的静态变量分配存储空间;
>
> ​      (3)解析:将符号引用转换成直接引用(这一步是可选的)
>
> 3.初始化:初始化静态变量，静态代码块。
>
> ​      这样的过程在程序调用类的静态成员的时候开始执行，所以静态方法main()才会成为一般程序的入口方法。类的构造器也会引发该动作。



##### 5.什么是反射

> Java反射机制是在运行状态时
>
> * 对于任意一个类都可以知道这个类的所有属性和方法
> * 对于任意一个对象都可以调用这个对象的任意属性和方法
>
> 这种动态获取信息、动态调用对象的任意属性和方法的功能称为Java语言的反射机制。
>
> ```java
> //Robot.java
> package com.Reflect;
> public class Robot{
>     private String name;
>     public void sayHi(String sentence){
>         System.out.println(sentence + " " + name);
>     }
>     private String sayHello(String tag){
>         return "Hello" + tag;
>     }
> }
> //ReflectSample.java
> public class ReflectSample{
>     public static void  main(String[] args) throws Exception{
>         //传入全类名
>         Class rc = Class.forName("com.Reflect.Robot");
>         Robot robot = (Robot)rc.newInstance;
>         System.out.println(robot.getName());
>         
>         //getDeclaredMethod可以获得任意访问权限的方法，但是不能获得继承和实现的方法	
>         Method sayHelloMethod = rc.getDeclaredMethod("sayHello",String.class);
>         //访问私有方法或属性要设置访问标识否则IllegalAccessException
>         method.setAccessible(true);
>        	Object str = method.invoke("Bob");
>         System.out.println(str);
>         
>         //getMethod只能获得public的方法，但是可以获得继承和实现的方法	
>         Method sayHiMethod = rc.getMethod("sayHi"，,String.class);
>         sayHi.invoke("hello");
>         
>         Field nameField =  rc.getDeclaredField("name");
>         name.setAccessible(true);
>         name.set("tom");
>         sayHi.invoke();
>     }
> }
> ```
>
> 结合实际项目更佳！！



6.5

