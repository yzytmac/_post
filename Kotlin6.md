---
title: Kotlin教程6---匿名函数和Lambda式
date: 2018-01-28 14:33:03
tags: Kotlin
categories: Kotlin教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517214609323&di=40d0cb3d0cacdcc718de20dccb81fa6d&imgtype=0&src=http%3A%2F%2Fimgup01.sj88.com%2F2017-06%2F30%2F01%2F1498755765289_0.jpg
---
### 在kotlin中匿名函数就真的只是没名字而已，Lambada表达式是真的Lambada

1、函数结构（函数类型）  
先了解一个概念函数结构。就是参数及类型，返回值及类型的一个组合,如:
```kotlin
fun funName(x:Int,y:Int):Int{return x-y}
```
那么这个方法的函数结构就是
```kotlin
(x:Int,y:Int)->Int  
```
那么匿名函数和Lambda表达式就是该函数结构对应的函数字面值，如：
```kotlin
fun add(arg:(x:Int,y:Int)->Int){......}  //有一个参数和返回值都是int型结构的函数作为参数，把整个函数结构作为一种数据类型来修饰该参数
```
2、Lambada表达式
```kotlin
add({a,b->a+b})  //大括号就是Lambda表达式
add(){a,b->a+b}  //当add方法的最后一个参数传lambada表达式时，lambda表达式可写在括号外面
add{a,b->a+b}  //小括号中不写东西时就可以省略了
```
3、匿名函数
```kotlin
add(fun(a:Int,b:Int):Int{return a+b})  //这种就是匿名函数，这个只能写在小括号中
```
* 注意：  
    1、kotlin中Lambda表达式总是被大括号括起来，参数列表无小括号  
    2、Lambda表达式可写在小括号中，小括号外，以及省略小括号都行  
    3、Lambda表达式的参数有用不上的可以用_代替。如：
    ```kotlin
    add（a,_->a+10）  
    ```
    4、如果该lambda表达式的参数只有一个，那么在函数体中可以用约定好的it来替代该参数，而且连->都可以省略。这样就变成了add{}这种形式。  

4、带接收者的匿名函数  
其实就是方法扩展的匿名形式，如：
```kotlin
//正常的方法扩展
fun A.haha(){}
//匿名的方法扩展就是
val haha = fun A.(){}
```
5、内联函数  
高阶函数会形成闭包，就是函数内的函数会持有函数的引用。每个函数都是对象，而内存的分配和调用都会造成大量开销。说人话就是函数的执行过程就是从调用处跳转到函数体的地址中，执行完函数体又回到调用处地址，这样来回是会耗费时间的，而高阶函数更甚，因为函数里面还有函数。为了减小这种时间上的开销，就有了内联函数，用inline修饰。  
他的原理就是将高阶函数的lambda表达式中的函数部分相当于直接复制到高阶函数体中，这样执行的时候就不会跳到lambda表达式所在的内存地址中去，就会减少一个来回的时间。
```kotlin
inline fun show(block:(String)->Unit){block("yzy")}
```
这个show函数就是个内联函数。由定义可知，内联函数是针对于高阶函数来说的，如果普通的函数仅仅是加个inline关键字修饰是不算内联函数的 。  
* 注意事项：像这种函数体小的高阶函数建议内联，而函数体较大的就不要用了。
内联函数不仅对函数产生影响，也对lambda表达式产生影响，都会把代码搞到函数调用点去，所以如果lambda表达式的函数体过大，不想内联，那么就可以用关键字noinline来修饰
```kotlin
inline fun show(block:(String)->Unit，noinline block2: () -> Unit){
    block("yzy")；
    block()
}
```

6、非局部返回  
高阶函数的lambda表达式中如果要return需注意。  
要么带标签return@funName 。funName就是高阶函数名，要带标签才能返回。
要么不带标签，那么该高阶函数必须是内联函数才可以。如上面的show函数。
```kotlin
show{str -> if (str == "yzy") return }。//就不需要带标签就可以直接返回
```