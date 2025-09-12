---
title: Kotlin语法初学2

cover: ./cover/Kotlin1.png
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

此外if表达式会返回分支内部代码块最后一个表达式的值
```kotlin
var numA: Int = 2
var numC: Int = if (numA > 2){
    numA++
    numA = 10
    println("numA > 2 => true")
    numA
}else if (numA == 2){
    numA++
    numA = 20
    println("numA == 2 => true")
    numA
}else{
    numA++
    numA = 30
    println("numA < 2 => true")
    numA
}
```
基于这一特性可以利用if表达式构建三目运算符：

```kotlin
var numB: Int = if ( numA > 2 ) 3 else 5
```

#### when语句

就相当于其他语言中的switch语句，可以匹配多个值，可以判断是否在某个范围内，可以判断是否不在某个范围内。

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
注意：Kotlin中when语句后面不用加break。

范围可以用a..b表示闭区间，也可以用a until b表示左闭右开区间。

也可以使用is判断参数类型

```kotlin
when (表达式) {
    is 数据类型 -> { // 代码块 } // 判断是否是某个类型
    !is 数据类型 -> { // 代码块 } // 判断是否不是某个类型
    else -> { // 代码块 } // 相当于default
}
```

when语句后如果不写括号，则可以当成一串if else语句来使用。

```kotlin
when {
    条件1 -> { // 代码块 }
    条件2 -> { // 代码块 }
    else -> { // 代码块 } //一定要加else
}
```

此外判断语句可以直接当做函数的返回值，不用写return关键字。

```kotlin
fun max(a: Int, b: Int): Int = if (a > b) a else b
```

### 循环语句

#### for语句

1. 基本
    - 递增(until,左闭右开)
    - 递减(downTo，闭区间)
    - 闭区间(..)
    - 步长(step)
  ```kotlin
  //输出0 1 2 3 4
  for (i in 0 until 5){
    print("i => $i \t")
  }
  //输出15 14 13 12 11
  for (i in 15 downTo 11){
    print("i => $i \t")
  }
  //输出20 21 22 23 24 25
  for (i in 20 .. 25){
    print("i => $i \t")
  }   
  //输出10 12 14
  for (i in 10 until 16 step 2){
    print("i => $i \t")
  }
```
2. 遍历
   `for(item in array){...}`
   ```kotlin
   val array = arrayOf(1, 2, 3, 4, 5)
   for(item in array){
       print(item)
   }
   for(item in array.indices){//.indices可以获取数组的所有合法索引值
       print(array[item])
   }
    for ((index,value) in array.withIndex()){  
        //把元素和它的索引打包成一个对象，可以一次拿到索引和值。
        println("index => $index \t value => $value")
    }
    ```


#### while语句和do-while语句与JAVA相同

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

## 参考资料
- [Kotlin 官方文档](https://kotlinlang.org/docs/reference/)
- [Kotlin——高级篇（一）：Lambda表达式详解](https://www.cnblogs.com/Jetictors/p/8647888.html)
- [Kotlin——初级篇（七）：函数（方法）基础总结](https://www.cnblogs.com/Jetictors/p/8506941.html)
- [Kotlin入门学习(非常详细)，从零基础入门到精通，看完这一篇就够了](https://blog.csdn.net/Javachichi/article/details/131677550?sharetype=blog&shareId=131677550&sharerefer=APP&sharesource=2301_80150902&sharefrom=link)

