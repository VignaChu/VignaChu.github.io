---
title: Kotlin语法初学3

cover: ../../cover/Kotlin1.png
date: 2025-09-12T12:12:52+08:00
lastmod: 2025-09-12T12:12:52+08:00
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
大三的课居然比大二还少，好耶

# 类与接口

## 类(class)

声明：class 类名 {}

### 构造函数

在Kotlin中，允许有一个主构造函数和多个二级构造函数。

#### 主构造函数

主构造函数是类头的一部分，它定义了类的属性和方法。主构造函数可以有默认参数，也可以有可变参数。

类内部会自动生成主构造函数对应的属性，并根据输入的值赋值。

构造函数只能包含初始化代码块`init{...}`,可以使用构造函数的参数。

```kotlin
    class Test private constructor(num: Int){
        init{

        }
    }
```

如果没有修饰词，则可以省略，直接写`class 类名{}`

#### 二级构造函数

二级构造函数以constructor关键字开头，可以有默认参数，也可以有可变参数。

```kotlin
    class Test{
        constructor(num: Int){

        }
    }
```

其中如果同时存在主构造函数和二级构造函数，则二级构造函数必须直接或间接委派给主构造函数。
class Test constructor(num: Int){

    init {
        println("num = $num")
    }
    // 这里将二级构造函数的参数num传给了主构造函数,先执行主构造函数，再执行二级构造函数
    constructor(num : Int, num2: Int) : this(num) {
        println(num + num2)
    }
}

### 类的实例化
类名(),不需要加new

### 类属性

类属性可以是val或var，且必须在后面声明类型，必须初始化。

```kotlin
    class Test{
        var name: String = "Kotlin"
        val age: Int = 25
        var isMarried: Boolean = false
        var height: Double? = null
    }
```
#### 后期初始化属性(lateinit)
可以使用`lateinit`关键字声明可延迟初始化var的非基本属性。本关键字允许将非空属性初始化为null，直到真正被初始化。将检查推迟到运行第一次时。
```kotlin
    class UserService {
        lateinit var repo: UserRepository   // 先不初始化

        fun init() {
            repo = UserRepository()         // 稍后注入
        }

        fun save(user: User) {
            repo.save(user)                 // 首次访问，若未初始化则抛异常
        }
    }
```

#### 懒加载(by lazy)
此外`by lazy{}`也可用于延迟初始化*(懒加载)*。可以将只读属性的初始化推迟到第一次真正被访问的时候，即**用的时候才开始赋值**。
```kotlin
    val data: String by lazy {        // 注意是 val
        println("compute!")
        "Hello"
    }

    fun main() {
        println("start")
        println(data)   // 这里才会打印 compute!，返回 Hello
        println(data)   // 直接拿缓存，不再打印 compute!
    }
```
#### 访问器(Getter/Setter)

在Kotlin中，属性自带getter和setter方法，用来控制怎么访存属性(做输入校验和输出格式化)。也可以自定义这些访问器。

```kotlin
    class Test{
        var name: String = "Kotlin"
        var age: Int = 25 
            get() = "my age is $field" 
            // 自定义getter方法
            set(value) {
                if(value > 0){ 
                    field = value 
                    //field表示属性原来的值，只能在访问器中使用，且只能用field给属性赋值。
                }
            }
    }
```

#### 常量属性(const)

在Kotlin中，可以用const关键字声明常量属性，常量属性的值在编译时就确定下来，不能再修改。

他只能是顶层变量或val属性,且类型只能是基本类型，值必须是字面变量或简单表达式(不能是函数调用或运行时再计算)

```kotlin
    const val APP_NAME = "MyApp"
    const val MAX_USERS = 100
    const val IS_DEBUG = true

    class Test{
        const val PI = 3.14159265358979323846
    }


    fun main() {
        println(APP_NAME) // 直接替换为字面量
    }
```
### 可视性修饰符

一共有四种:public(公有)、private(私有)、internal(模块)、protected(保护)，取消了JAVA的包可见

类外只可访问public/internal修饰的类.接口内只能有public修饰的成员。

如果private修饰主构造，则无法新建实例，在单例中使用。

getter/setter的能见度不能高于属性本身。

### 继承

**面向对象有三大特性：封装、继承、多态。——————不是淳平**

在kotlin中，只有继承类(open)可以被继承，类和成员都需要`open`关键字：

```kotlin
    open class Animal{
        open fun eat(){
            println("animal is eating")
        }
        open var name: String = "animal"
    }
```

类的继承需要在类名的后面加`类名 : 父类名`
```kotlin
    class Dog : Animal(){
        override fun eat(){   
          // 重写父类方法，override不可省略
            println("dog is eating")
        }
        override var name: String = "dog"
    }
```

#### 构造函数

子类可以重写父类的构造函数，但不能调用父类的构造函数。
1. 无主构造函数：
   
每个二级构造函数必须使用:super初始化基类型
```kotlin
    class MyView : View(){

        constructor(context: Context) : super(context)

        constructor(context: Context, attrs: AttributeSet?) : super(context, attrs)

        constructor(context: Context, attrs: AttributeSet?, defStyleAttr: Int)
            : super(context, attrs, defStyleAttr)
    }
```
2. 存在主构造函数
  
主构造函数实现基类型最多的构造函数，其他的情况用this引用
```kotlin
    class MyView(context: Context?, attrs: AttributeSet?, defStyleAttr: Int)
      : View(context, attrs, defStyleAttr) {

      constructor(context: Context?) : this(context,null,0)
      
      constructor(context: Context?,attrs: AttributeSet?) : this(context,attrs,0)
  }
```

### 对象表达式

**对象表达式**是kotlin中创建匿名内部类的快捷方式
```kotlin
object : 父类(构造函数调用顺序参数)/接口,··· {
    // 重写方法、定义属性、定义函数等
}
```

不能定义构造函数。

# 枚举类

## 定义：
```kotlin
enum class Color {
    RED, GREEN, BLUE
}
```
每个枚举常量都有两个属性：name(名称)和ordinal(位置)，通过枚举类名.常量名.属性名访问。
```kotlin
val color = Color.RED
println(color.name) // RED
println(color.ordinal) // 0
```
## 枚举常量的具体实现

枚举类可以带抽象方法，并且每个枚举常量需要实现它。
```kotlin
enum class Operation {
    // 为每个常量提供抽象方法的具体实现
    PLUS {
        override fun calculate(a: Int, b: Int): Int = a + b
    },
    MINUS {
        override fun calculate(a: Int, b: Int): Int = a - b
    },
    TIMES {
        override fun calculate(a: Int, b: Int): Int = a * b
    },
    DIVIDE {
        override fun calculate(a: Int, b: Int): Int = a / b
    };

    // 抽象方法，必须在每个常量中实现
    abstract fun calculate(a: Int, b: Int): Int
}
```
# 接口

interface 接口名 {
    // 接口中的属性、方法、函数
}

接口可以有属性、方法、函数，但不能有构造函数。

接口可以继承其他接口，但不能继承类。

接口的属性要么没有初始值，要么通过自定义setter方法初始化。

接口的实现类必须实现接口的所有方法。

# 其他

## 数据类

### 定义

数据类是一种特殊的类，它自动生成了equals()、hashCode()、toString()方法，并且提供了copy()方法。
```kotlin
data class User(val name: String, val age: Int){
    var address: String = "",
    var phone: String = "",
    //此时类中已经有了name,age,address,phone属性。
}
```

### 特性

1. 主构造函数必须有参数
2. 不能是抽象类、密封类或内部类等。
3. 可以实现接口，且可以继承自密封类。
4. 数据类也可以进行解构处理
```kotlin
val (name, age, address, phone) = user
```

### 修改

数据类的修改需要用到自动定义的copy()方法。
```kotlin
val user = User("Tom", 25)
user.address = "China"
val newUser = user.copy(age = 26)   
```
### 特殊的的默认数据类

这些数据类默认被定义好，一常规的数据类有着实现上的不同处，有着一些独特的特性，而且不需要额外的创建类的开销。但是均为不可变值。

#### Pair

Pair是一个数据类，它有两个属性：first和second。能够存储两个不能变的值。

**定义方式**:
1. `var pair = Pair(1, "Hello")`
2. `val pair = 1 to "Hello" //为pair特有的语法糖`
   

#### Triple

Triple是一个数据类，它有三个属性：first、second和third。能够存储三个不能变的值。

**定义方式**:
1. `var triple = Triple(1, "Hello", true)`
2. `val triple = 1 to "Hello" to true //为triple特有的语法糖`
   
此外，两者的tostring()方法也和常规的数据类有所不同。

## 密封类

密封类是一种特殊的类，不能被实例化,只可以被继承或构造单例对象。子类都在一个文件中定义。

```kotlin
sealed class Shape
```

密封类的子类和单例对象只有有限的几种可能，可以用来条件判断的检查。同时能够表示选项和携带数据。


## 抽象类、内部类

和JAVA差不多就不说了

## 委托

委托类似于java中的组合类，通过关键字**by**来实现。重点在于一个类委托某个实现了接口的类实现这个接口的功能

语法：
```kotlin
class A(b: B) : SomeInterface by b{
    ...
}
```
这样A具有了SomeInterface的全部方法，并且可以调用A自己的方法。

# 参考资料
- [Kotlin——中级篇（一）：类（class）详解](https://www.cnblogs.com/Jetictors/p/7758828.html)
- [一文彻底搞懂Kotlin中的委托](https://juejin.cn/post/6844904038589267982)
