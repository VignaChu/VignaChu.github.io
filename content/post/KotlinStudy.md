---
title: Kotlin语法初学

cover: ./cover/Kotlin1.png
date: 2025-08-27T23:12:52+08:00
lastmod: 2025-08-27T23:12:52+08:00
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

## 关于Kotlin
Kotlin是一种现代的编程语言，由JetBrains开发，旨在提高开发效率和代码可读性。它与Java高度兼容，可以运行在JVM上，并且可以与Java代码无缝互操作。Kotlin的设计目标是简化代码，减少样板代码，并提供更强大的功能，如空安全、扩展函数和协程等。Java开发者可以很容易地学习Kotlin，因为Kotlin与Java有着良好的互操作性。并且Kotlin可以编译为JS代码，可以运行在浏览器上。

Kotlin的语法与Java非常相似，但有一些重要的区别。例如，Kotlin不允许使用`public`、`protected`、`static`和`final`修饰符，并且要求在声明变量时初始化。Kotlin的类型系统更加严格，并有着更强大的功能，如可空性和扩展函数。Kotlin支持函数式编程，允许使用高阶函数、lambda表达式和内联函数。Kotlin支持数据类、委托、接口、注解、泛型、协程等。

## 语法

### 基础语法

kotlin代码以`.kt`为后缀，需要一个main函数作为入口，同时代码尾部不需要分号，用fun关键字定义函数。

```kotlin
fun main() {
    println("Hello, world!")
}
```

#### 注释

单行注释以`//`开头，多行注释以`/*`开头，并以`*/`结尾。

```kotlin
// This is a single-line comment.

/*
This is a
multi-line comment.
*/
```

#### 标识符

Kotlin 的标识符遵循与 Java 相同的命名规则，但有两个主要例外：  
1. Kotlin 不允许单独使用下划线 `_` 作为标识符（从 Kotlin 1.5 起已保留为关键字）；  
2. Kotlin 不允许使用任何关键字或保留字作为标识符。

```kotlin
// 合法的标识符
val name = "Kotlin"
val _name = "Kotlin"
val name1 = "Kotlin"

// 非法的标识符
val 1name = "Kotlin" // 数字开头在JAVA中即不行
val name@ = "Kotlin"
```

#### 变量声明

kotlin通过var关键字声明变量，通过val关键字声明常量。默认为自动类型推断，在变量名后面加:数据类型可以显式声明变量的数据类型。

1. 声明变量时初始化：

```kotlin
val name = "Kotlin"
val age: Int = 25
```

2. 声明变量时不初始化：

```kotlin
var name: String
var age: Int
// 这种情况必须显式声明数据类型，因为不能从初始化的数据中推断(如：age = 25)
```

3. 声明常量：

```kotlin
val PI = 3.14159
```

#### 数据类型

Kotlin 支持以下数据类型：

- **基本类型**：`Int`、`Long`、`Short`、`Byte`、`Float`、`Double`、`Char`、`Boolean`
- **字符串类型**：`String`
- **数组**：
  - 基本类型数组：`IntArray`、`LongArray`、`FloatArray`、`DoubleArray`、`BooleanArray`、`CharArray`、`ByteArray`、`ShortArray`
  - 泛型数组：`Array<T>`
- **列表、集合、映射**（只读接口及其可变版本）：
  - 只读：`List`、`Set`、`Map`
  - 可变：`MutableList`、`MutableSet`、`MutableMap`
- **类**：`class`、`object`
- **接口**：`interface`
- **注解**：`annotation class`

要建立只读列表，可以使用`listOf()`函数，建立可变列表，可以使用`mutableListOf()`函数。其余两者替换方法中对应的名称即可。

```kotlin
val list = listOf(1, 2, 3)
val mutableList = mutableListOf(1, 2, 3)
```

并通过 *[]*访问列表中的元素，*.first()*和 *.last()*方法可以访问列表的第一个和最后一个元素, *.count()*方法可以获取列表的长度。
```kotlin
println(list[0]) // 1
println(list.first()) // 1
println(list.last()) // 3
println(list.count()) // 3
```


使用**in**运算符可以判断元素是否在列表中。
```kotlin
if (1 in list) {
    println("1 is in the list")
}
```

使用 *.add()*方法可以向列表中添加元素, *.remove()*方法可以删除元素。

获取映射中是否有对应的键，可以使用 *.containsKey()*方法，获取映射中是否有对应的值，可以使用 *.containsValue()*方法。

*太困了，先写到这里了，晚安Zzz*

## 参考资料
- [Kotlin 官方文档](https://kotlinlang.org/docs/reference/)

