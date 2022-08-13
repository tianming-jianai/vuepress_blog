---
prev: /java/
next: /java/
---

# Java 8 新特性

> TITLE：Springboot零基础到项目实战
>
> AUTHOR：黎老师
>
> SCHOOL：
>
> VIDEO：[黎曼的猜想 - 宋红康](https://www.bilibili.com/video/BV184411x7XA)
>
> FILE：
>
> GITHUB：[学习SpringBoot](https://github.com/tianming-jianai/jdkfeature)

相关： [ Java学习笔记目录索引 (持续更新中)_Guizy-CSDN博客](https://blog.csdn.net/m0_37989980/article/details/103987924)



## 学习进度

- 开始时间：2022-08-13
- 结束时间：

|    日期    | 课程编号 | 学习时长 |
| :--------: | :------: | :------: |
| 2022-08-13 |  P1~P10  |    2h    |
|            |          |          |
|            |          |          |

- 复习

| 日期 | 内容 |
| ---- | ---- |
|      |      |



![java8新特性](java8.png)

- 学习的思维方式：
  - 大处着眼、小处着手
  - 逆向思维、反证法
  - 透过问题看本质

- 两句话：
  - 小不忍则乱大谋
  - 识时务为俊杰

- 技术书：和其他类书籍的思维方式不同

（读经济学：（研究人的行为）生活中的经济学，宏观、围观经济学，博弈论）

## java 8 新特性

- 速度更快（红黑树...）
- 代码更少（增加了新的语法：**lambda表达式**）
- 强大的**Stream API**
- 便于并行
- 最大化减少空指针异常：Optional
- Nashorn引擎：允许在JVM上允许JS应用

java语言不一定是世界上最强大的语言，但是java虚拟机一定是目前世界上最强大的虚拟机

## 一、 Lambda 表达式

Lambda是一个匿名函数，我们可以把 Lambda表达式理解为是**一段可以传递的代码**将代码像数据一样进行传递）。使用它可以写出更简洁、更灵活的代码。作为一种更紧凑的代码风格，使Java的语言表达能力得到了提升。

- 代码示例

```java
Runnable r = () -> System.out.println("我爱北京天安门");
r.run();
```

```java
Comparator<Integer> comp = (c1,c2) -> Integer.compare(c1,c2);
int res = comp.compare(1, 1);
System.out.println(res);
```

```java
// 方法引用
Comparator<Integer> comp2 = Integer::compare;
int res2 = comp2.compare(3, 2);
System.out.println(res2);
```



左边：接口抽象方法的形参

右边：重写抽象方法的方法体

本质：**作为接口的实例**（**函数式接口只有一个抽象方法**）

如果一个接口中只声明了一个抽象方法，name这个接口就可以被称为函数式接口

- 六中情况下使用Lambda表达式

1. 无参，无返回值

2. 一个参数，没有返回值

   ```java
   Consumer<String> con = param -> System.out.println(param);
   Consumer<String> con2 = System.out::println;
   con.accept("abc");
   con2.accept("ABC");
   ```

3. 类型推断

4. 参数只有一个，小括号不用写

5. 两个参数及以上，可以有返回值

6. 只有一条执行语句，可省略大括号，有返回值return也不用写

### 1. 什么是函数式接口

- **只包含一个抽象方法的接口，称为函数式接口**
- 你可以通过lambda表达式来创建该接口的对象。（若lambda表达式抛出一个受检异常（即：非运行时异常），那么该异常需要在目标接口的抽象方法上声明）
- 我们可以在一个接口上使用**@FunctionalInterface**注解，这样可以检查它是否是一个函数式接口。同时也会包含一条声明，说明这个接口是一个函数式接口。
- **在java.util.function包下定义了java8的丰富的函数式接口**

java不但可以支持OOP还可以支持OOF（面向函数编程）

java8中，lambda表示是对象，而不是函数，它们必须依附于一类特别的对象——函数式接口

lambda表达式就是一个函数式接口的实例

所以以前用匿名实现类表示的现在都可以用lambda表达式来写

### 2. java内置四大函数式接口

| 函数式接口                | 参数类型 | 返回类型 | 用途                                                         |
| ------------------------- | -------- | -------- | ------------------------------------------------------------ |
| Consumer<T><br />消费型   | T        | void     | 对类型T的对象应用操作，包含方法 **void accept(T t)**         |
| Supplier<T><br />供给型   | 无       | T        | 返回类型为T的对象，包含方法**T get()**                       |
| Function<T,R><br />函数型 | T        | R        | 对类型为T的对象应用操作，并返回结果。结果是R类型的对象。包含方法**R apply(T t)** |
| Predicate<T><br />断定型  | T        | boolean  | 确定类型为T的对象是否满足某约束，并返回boolean的值，包含方法**boolean test(T t)** |

```java
package com.zsg.chapter01;

import org.junit.jupiter.api.Test;

import java.sql.Array;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Predicate;

/**
 * @BelongsProject: jdkfeature
 * @BelongsPackage: com.zsg.chapter01
 * @Author: 张世罡
 * @CreateTime: 2022/8/14 1:27
 * @Description:
 */
public class LambdaTest2 {
    /**
     * 测试 消费型
     */
    @Test
    public void test1() {
        happyTime(2D, new Consumer<Double>() {
            @Override
            public void accept(Double money) {
                System.out.println(String.format("花%.0f块钱买了瓶可乐", money));
            }
        });

        happyTime(30D, money -> System.out.println(String.format("花%.2f元，玩了把真人模拟射击", money)));
    }

    public void happyTime(Double money, Consumer<Double> consumer) {
        consumer.accept(money);
    }

    /**
     * 测试 断定型
     */
    @Test
    public void test2() {
        List<String> list = Arrays.asList("北京", "南京", "天津", "东京", "普京");
        List<String> filterResult = filterString(list, new Predicate<String>() {
            @Override
            public boolean test(String s) {
                return s.contains("京");
            }
        });
        System.out.println(filterResult);

        System.out.println(filterString(list, s -> s.contains("京"));
    }

    public List<String> filterString(List<String> list, Predicate<String> predicate) {
        ArrayList<String> newList = new ArrayList<>();
        for (String s : list) {
            if (predicate.test(s)) {
                newList.add(s);
            }
        }
        return newList;
    }
}
```

### 3. 方法引用与构造器引用

#### 方法引用

- 当要传递给lambda体的操作，**已经有实现方法了，可以使用方法引用**
- 方法引用可以看做是lambda表达式深层次的表达，换句话说，方法引用就是lambda表达式，也就是函数式接口的一个实例，通过方法名来指向一个方法，可以认为是lambda的一个语法糖
- 要求：**实现接口的抽象方法的参数列表和返回值类型，必须与方法引用的方法的参数列表和返回值类型保持一致！**
- 格式：双引号"**::**"
- 三种情况
  - **对象::实例方法名**
  - **类::静态方法名**
  - **类::实例方法名**
- 方法引用使用要求，要求接口中的抽象方法的形参列表（和）返回值类型 与 方法引用的方法形的参列表（和）返回值类型相同！



- 代码示例

```java
/**
* 情境一： 对象：实例方法
* Consumer     void accept(T t)
* PrintStream  void println(T t)
*/
@Test
public void test1() {
    Consumer<String> con = str -> System.out.println(str);
    con.accept("北京");

    PrintStream ps = System.out;
    Consumer<String> con2 = ps::println;
    con2.accept("天安门");
}

/**
* Supplier void get()
* Employee void getName()
*/
@Test
public void test2() {
    Employee emp = new Employee(1001, "Tom", 23, 5600);
    Supplier<String> sup1 = () -> emp.getName();
    System.out.println(sup1.get());

    Supplier<String> sup2 = emp::getName;
    System.out.println(sup2.get());
}
```

- 代码示例

```java
/**
* 情境二 类 :: 静态方法
* Comparator   int compare(T t1, T t2)
* Integer      int compare(T t1, T t2)
*/
@Test
public void test3() {
    Comparator<Integer> com = (t1, t2) -> Integer.compare(t1, t2);
    System.out.println(com.compare(1, 2));

    Comparator<Integer> com2 = Integer::compare;
    System.out.println(com2.compare(2, 1));
}

/**
* Function R apply(T t)
* Math     long round(Double d)
*/
@Test
public void test4() {
    Function<Double, Long> func = d -> Math.round(d);
    System.out.println(func.apply(12.3));

    Function<Double, Long> func2 = Math::round;
    System.out.println(func2.apply(12.6));
}
```

- 代码示例

```java
/**
* 情况三 类 :: 实例方法
* Comparator   int compare(T t1, T t2)
* String       int t1.compareTo(t2)
*/
@Test
public void test5() {
    Comparator<String> comp = (s1, s2) -> s1.compareTo(s2);
    System.out.println(comp.compare("abc", "abd"));

    Comparator<String> comp2 = String::compareTo;
    System.out.println(comp2.compare("abd", "abc"));
}

/**
* BiPredicate  boolean test(T t1, T t2)
* String       boolean t1.equals(t2)
*/
@Test
public void test6() {
    BiPredicate<String, String> pre = (s1, s2) -> s1.equals(s2);
    System.out.println(pre.test("abc", "abd"));

    BiPredicate<String, String> pre2 = String::equals;
    System.out.println(pre2.test("abd", "abd"));
}

/**
* Function R apply(T t)
* Employee String getName()
*/
@Test
public void test7() {
    Employee employee = new Employee();
    employee.setName("Jack");
    Function<Employee, String> func = e -> e.getName();
    System.out.println(func.apply(employee));

    Function<Employee, String> func2 = Employee::getName;
    System.out.println(func2.apply(employee));
}
```
