---
title: Kotlin语法初学

cover: ./cover/Kotlin1.png
date: 2025-08-28T23:12:52+08:00
lastmod: 2025-08-28T23:12:52+08:00
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

**注意：**kotlin全部使用对象类型，不再存在基本类型。

##### 数组

创建数组：
1. arrayOf()
  
```kotlin
var arr = arrayOf("0","2","3",'a',32.3f)
for (v in arr){
    print(v)
    print("\t")
}
```

同时也可以用这个方法同时为多个变量赋值`val (x, y, z) = arrayOf(10, 20, 30)`

2. arrayOfNulls()

```kotlin
var arr3 = arrayOfNulls<Int>(3)

//如若不予数组赋值则arr3[0]、arr3[1]、arr3[2]皆为null
for(v in arr3){
    print(v)
    print("\t")
}
```
输出结果`null	null	null	`

3. Array()
   参数为元素个数以及一个函数，以索引为参数返回函数值
```kotlin
val arr2 = Array(5){i -> i*i}
for(v in arr2){
    print(v)
    print("\t")
```
结果为`0 1	4	9	16`



其中还有各种封装好的原始类型的数组：
1. ByteArray => 表示字节型数组
2. ShortArray => 表示短整型数组
3. IntArray => 表示整型数组
4. LongArray => 表示长整型数组
5. BooleanArray => 表示布尔型数组
6. CharArray => 表示字符型数组
7. FloatArray => 表示浮点型数组
8. DoubleArray => 表示双精度浮点型数组

数组方法:
1. arr.sort() => 排序
2. arr.forEach { println(it) } => 遍历数组
3. arr.filter { it > 2 } => 过滤数组
4. arr.reverse() => 反转数组
5. arr.shuffle() => 随机排序数组
6. arr.fill(a) => 填充数组为a
7. 数组中+为拼接数组，-为删除数组中与另一个数组相同的元素
8. arr.slice(1..3) => 切片数组
   ```kotlin
   val ori = arrayOf("a", "b", "c")
   val doubled = ori + ori        // 返回新数组 ["a","b","c","a","b","c"]
   val slice = ori.copyOfRange(1, 3) // ["b","c"]
   ```
9. arr.sum() => 计算数组元素的和
10. arr.average() => 计算数组元素的平均值

使用`XXXArrayOf()`赋初始值

##### 字符串
''' '''为可以包含任何字符的字符串，不会被转义。

在双引号中使用$变量名或${表达式}为字符串模板，

##### 列表、集合、映射

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

#### 位运算

Kotlin与JAVA不同，没有特殊的符号用于位运算，而是采用自带函数(仅用于Int和Long):

1. shl(bits) => 有符号向左移 (类似Java的<<)
2. shr(bits) => 有符号向右移 (类似Java的>>)
3. ushr(bits) => 无符号向右移 (类似Java的>>>)
4. and(bits) => 位运算符 and (同Java中的按位与)
5. or(bits) => 位运算符 or (同Java中的按位或)
6. xor(bits) => 位运算符 xor (同Java中的按位异或)
7. inv() => 位运算符 按位取反 (同Java中的按位取反)


*太困了，先写到这里了，晚安Zzz*

## 参考资料
- [Kotlin 官方文档](https://kotlinlang.org/docs/reference/)

