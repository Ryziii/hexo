---
title: core java笔记(第四章-对象与类)
date: 2018-09-28 13:25:23
tags:
	- core java
	- java
---

1. **方法重载:**

   - 概述:在同一个类中，允许存在一个以上的同名方法，只要它们的参数个数或者参数类型不同即可。
   - 特点:与返回值类型无关，只看方法名和参数列表
     在调用时，虚拟机通过参数列表的不同来区分同名方法”

1. **java数组长度：**

   ​	java数组长度可以为0，0时非null。如果数组为null如果对数组进行操作会报NullPointException，在以数组返回的方法中如果返回没有值则一般返回长度为0的数组这样对方法调用者对其作处理比较方便。

1. **对象变量与对象：**

   对象变量知识对对象的一个引用，不能调用对象的方法，如下：

    ```java
    Date deadline;
    deadline.toString();//错误
    deadline = new Date();
    deadline.toString();//正确
    ```

1. **返回可变对象：**

	getter返回对象如果是可变对象类型因为返回对象的克隆，否则破坏封装型。

    ```java
    class Employee
    {
        ...
        public Date getHireDay()
        {
            return hireDay;
        }
    }
    Employee harry=...;
    Date d = harry.getHireDay();
    d.setTime(.....);
    //此时可以更改封装类中的数据hireday
    //getHireDay更改为如下形式即可
    class Employee
    {
        ...
        public Date getHireDay()
        {
            return (Date)hireDay.clone();
        }
    }
    
    ```

1. **final:**

	一般修饰不可变类型，如String而非StringBuilder。如果修饰可变类就会发生混乱。

1. **static 静态：**

     static不依赖对象，可以在没创建对象的情况下通过类名调用(方法／对象)。

     1. 静态方法：

        - 一个方法不需要访问对象状态所有参数都是显式参数提供的（Math.pow)

        - 一个方法只需要访问类的静态域(Employee.getNextId)

     1. 静态变量：被所有对象拥有，只有一个副本

     1. 静态代码块：可用于优化性能

        ```java
        //对比两个代码
        class Person{
            private Date birthDate;
             
            public Person(Date birthDate) {
                this.birthDate = birthDate;
            }
             
            boolean isBornBoomer() {
                Date startDate = Date.valueOf("1946");
                Date endDate = Date.valueOf("1964");
                return birthDate.compareTo(startDate)>=0 && birthDate.compareTo(endDate) < 0;
            }
        }
        //上个代码每次调用isBornBoomer时会生成startDate和endDate对象 造成资源浪费，使用下个代码则只在类初始化时调用一次
        class Person{
            private Date birthDate;
            private static Date startDate,endDate;
            static{
                startDate = Date.valueOf("1946");
                endDate = Date.valueOf("1964");
            }
             
            public Person(Date birthDate) {
                this.birthDate = birthDate;
            }
             
            boolean isBornBoomer() {
                return birthDate.compareTo(startDate)>=0 && birthDate.compareTo(endDate) < 0;
            }
        }
        ```

1. **java swap：**

   java方法中式对对象值的传递，也就是c中的形参，不是实参。所以swap后不会改变原来对象的值，如果更改的是对象的属性则可以改变。

   ```java
   //这个方法不会改变传入的原对象的值
   public static swapObject(Test a,Test b){
    Test c;
    c = b;
    b = a;
    a = c;
   }
   //此方法可以改变对象的属性
   public static swapObjectProperty(Test a ,Test b ){
    Test c;
    c.num = b.num;
    b.num = a.num;
    a.num = c.num;
   }
   ```

1. **构造器：**

   当类为提供构造器时才会由系统提供一个默认构造器(将所有属性初始化)，如果写了一个构造器，则无默认构造器

   构造器中使用this(...)是指使用构同一个类中的另一个构造器

   ```java
   public Employee(double d){
       this("aaa",3.33);
   }
   //这个this()指的就是调用同个类下的另一个构造器Employee(String,double)
   ```
