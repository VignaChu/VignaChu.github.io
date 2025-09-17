---
title: Kotlin语法初学4
draft: true  // 草稿
cover: ../../cover/Kotlin1.png
date: 2025-09-16T19:50:52+08:00
lastmod: 2025-09-15T12:12:52+08:00
tags:
  - Android
  - Study
  - Kotlin
categories:
  - Study

math: true
mermaid: true

---

# 杂谈 
今天应该是最后一天学kotlin的基本语法了，主要是查缺补漏，把剩余的知识点都集中在这篇中，所以可能篇幅比较长。

# 标准高阶函数

## run{}函数

- 功能：执行一个代码块(即唯一参数lambda表达式)，并返回该代码块的最后一行表达式的值。
```kotlin
fun main() {
    val result = run {
        println("Hello, world!")
        42
    }
    println(result)
}
```
## T.run

- 功能：附着在一个标识符后面，执行代码块，并可以用this来引用该标识符。
```kotlin
fun main() {  
    val result = "Hello, world!".run { // .的优先级大于=
        println(this)
        println(length)
    }
    println(result)
}
```
## T.with()函数

- 功能：将一个代码块(即唯一参数lambda表达式)应用到一个对象上，并返回该代码块的最后一行表达式的值。
```kotlin
fun main() {
    val result = with(StringBuilder()) {
        append("Hello, ")
        append("world!")
        length
    }
    println(result)
}
```

## T.apply{}函数

- 功能：执行一个代码块(即唯一参数lambda表达式)，并返回附着的对象。
```kotlin
fun main() {
    val sb = StringBuilder().apply {
        append("Hello, ")
        append("world!")
    }
    println(sb.length)
}
```


## T.also{}函数

- 功能：执行一个代码块(即唯一参数lambda表达式)，并返回自身对象。

- 与apply()函数的区别：also()用it表示自身，而apply()用this表示自身。

## T.takeIf{}函数

- 功能：如果一个对象满足代码块内给定的条件，则返回该对象，否则返回null。

```kotlin
val str = "kotlin"

val result = str.takeIf {
    it.startsWith("ko") 
}

println("result = $result")
```

## T.takeUnless()

- 功能：与上一个相反

## repeat(n){···}

- 功能：重复执行n次后加代码块的代码。

# 泛型

1. 基础语法

```kotlin
class Box<T>(t: T) {
    var value = t
}
```


# 参考资料

- [Kotlin——高级篇（二）：高阶函数详解与标准的高阶函数使用](https://www.cnblogs.com/Jetictors/p/9225557.html)
- [Kotlin（六）深入理解Kotlin泛型](https://juejin.cn/post/6959859571242303495)
- [Android 上的 Kotlin 协程](https://developer.android.google.cn/kotlin/coroutines?hl=zh-cn)
- [Null safety](https://kotlinlang.org/docs/kotlin-tour-null-safety.html)
- [中级：库和 API](https://kotlinlang.org/docs/kotlin-tour-intermediate-libraries-and-apis.html)