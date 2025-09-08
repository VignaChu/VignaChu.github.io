---
title: Kotlin语法初学2

cover: ./cover/Kotlin2.png
date: 2025-09-06T12:12:52+08:00
lastmod: 2025-09-06T12:12:52+08:00
tags:
  - Android
  - Study
  - Kotlin
categories:
  - Study

math: true
mermaid: true

---

## 杂谈
由于前几天一直生病，所以没能够及时更新，从今天开始继续。

## 语法

### 判断语句

#### if语句

格式：

```kotlin
if (条件表达式) { // 条件成立执行的代码块
    // 代码块
} else if (条件表达式) { // 条件成立执行的代码块
    // 代码块 
} else { // 条件都不成立执行的代码块    
    // 代码块
}
```

#### when语句

格式：

```kotlin
when (表达式) {
    值1 -> { // 代码块 }
    值2, 值3 -> { // 代码块 } // 多个值使用逗号分隔
    in 范围 -> { // 代码块 } // 判断是否在某个范围内
    !in 范围 -> { // 代码块 } // 判断是否不在某个范围内
    else -> { // 代码块 } // 相当于default
}
```



### 函数

#### 函数声明

1.一般情况:

fun 函数名(参数: 数据类型): 返回值类型 {
    函数体
}

**注1:** Kotlin中无返回值可以写成*Unit*

**注2:** Kotlin中存在*类型推导*，可以省略数据类型。

**注3:** Kotlin中默认参数值在数据类型后面加上 *=默认值* 即可。

```kotlin
fun defArgs(numA : Int  = 1, numB : Float = 2f, numC : Boolean = false){
    println("numA  =  $numA \t numB = $numB \t numC = $numC")
}
```

在调用有默认值的函数时，可以在参数内写*参数名 = 参数*来指定为某个参数赋值，未指定的参数会使用默认值。

```kotlin 
defArgs(numA = 3, numC = true) // numB使用默认值
```
2.单行函数:

fun 函数名(参数: 数据类型) = 函数体

3.可变参数函数:

格式：fun 函数名(vararg 参数名 ： 类型，...) ：返回值{}

```kotlin
fun printAll(vararg messages: String) {
    for (m in messages) println(m)
}

// 调用
printAll("Hello", "World", "Kotlin")

var array = arrayOf("Hello", "World", "Kotlin")
printAll(*array) // 解包数组,需要使用*展开运算符
```

注意：只能有一个可变参数，且最好放在最后一个参数，否则后面定义的参数需要指定参数赋值。

4.lambda表达式:

定义：

1. { 参数 -> 函数体 } // 无参数参数箭头可省略
2. (参数)->返回值类型=  {函数体}

特殊情况：

1. it在lambda表达式中代表默认的唯一参数。
```kotlin
{println(it)} //等价于 {a -> println(a)}
```

2. _在lambda表达式中代表忽略的唯一参数。
```kotlin
{_, b -> println(b)} // 忽略第一个参数

val sum = {a: Int, b: Int -> a + b}
println(sum(1, 2)) // 3
```

5. 匿名函数:

格式：fun (参数)->返回值类型 = {表达式}

```kotlin
val add = fun(x: Int, y: Int): Int {
    return x + y
}
```

### 类

#### 类声明

格式：

```kotlin
class 类名{
    // 构造函数
    constructor(参数: 数据类型){
        // 函数体
    }

    // 成员变量
    var 变量名: 数据类型 = 初始值

    // 成员函数
    fun 函数名(参数: 数据类型): 返回值类型{
        // 函数体
    }
}
```

#### 继承

格式：

```kotlin
class 子类名 : 父类名{
    // 构造函数
    constructor(参数: 数据类型){
        // 函数体
    }

    // 成员变量
    var 变量名: 数据类型 = 初始值

    // 成员函数
## 参考资料
- [Kotlin 官方文档](https://kotlinlang.org/docs/reference/)

