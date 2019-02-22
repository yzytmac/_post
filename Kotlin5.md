---
title: Kotlin教程5---条件语句
date: 2018-01-28 14:32:03
tags: Kotlin
categories: Kotlin教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517214609323&di=40d0cb3d0cacdcc718de20dccb81fa6d&imgtype=0&src=http%3A%2F%2Fimgup01.sj88.com%2F2017-06%2F30%2F01%2F1498755765289_0.jpg
---
### if else、while(){}、do{}while()、for循环

1、简单for循环
```kotlin
for(i in 0..10){} //从0到10，包含10。i in 0 until 10不包含10
for(i in 10 downTo 0) // 从10到0
for(i in 0..10 step 2)  //每2个一迭代（0，2，4，6，8，10）
for(i in 0..10 step 3)  //每3个一迭代（0，3，6，9）
```
* in表示在某个区间，！in表示不在某个区间  

迭代for循环
```kotlin
for(item in collection){}  //迭代其中的元素
```
得到索引
```kotlin
for (i in array.indices) {} //得到索引
```
增强的
```kotlin
for((index,value) in collect.withIndex())  //得到索引和值
```
2、when语句  
比switch-case更加强大.甚至可以将整个when语句块作为返回值return出去
```kotlin
when(x){
    1 -> print("x is "+1)
    2,3,4-> print("x is 2 or 3 or 4") 
    in 5..10 -> print("x is 5<=x<=10")
    parseInt("11") -> print("x is 11")
    !in 12..15->print("x is not in 12 to 15")
    else -> print("unknow")
}
```
还可以不传参数当if else来用
```kotlin
when{
    x>5 -> print("x is bigger than 5")
    x<10 -> print("x is less than 10")
    else -> print("unkonw")
}
```
3、函数嵌套。支持break、continue、return以及标签  
加标签：tabName@  
使用标签：
```kotlin
break@tabName 、continue@tabName 、return@tabName 、return@tabName 
```
4、作用域函数with，如：
```kotlin
class Person{
    fun eat(){}
    fun speak(){}
    fun look(){}
}
val p = Person()
//调用Person对象的三个方法。正常情况下我们用p点方法名，这里有了with就可以省略了
with(p){
    //这三个方法的范围就是Person对象，所以前面就可以省略对象点了
    eat()
    speak90
    look()
}
```
