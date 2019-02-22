---
title: Kotlin教程3---空安全
date: 2018-01-28 14:30:03
tags: Kotlin
categories: Kotlin教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517214609323&di=40d0cb3d0cacdcc718de20dccb81fa6d&imgtype=0&src=http%3A%2F%2Fimgup01.sj88.com%2F2017-06%2F30%2F01%2F1498755765289_0.jpg
---
1、在kotlin中是不允许直接为空的，如：
```kotlin
var a:String = null
```
2、但是有些变量确实会存在空，那就要特殊标记允许为空  
如果a真的可能为空那就再声明的时候用问号？标记如：
```kotlin
var a:String？ = null	？的意思就是可为空
```
3、安全的调用  
那如果调用a.length方法就可能空指针。编译器会在编译阶段就报错，我们就要做非空检测
```kotlin
if(a!=null) a.length
```
这种事显式的检测。那么隐式的就是安全的调用 ?.  
如：
```kotlin
a?.length
```
 意思就是如果a非空就直接调length，a为空就直接返回null

4、Elvis 操作符  ?:  
类似于java中的三元运算符
```kotlin
a?.func() ?: print( "左边空啦")
```
意思就是如果?:左边出现空指针，那么就执行右边的表达式。

5、!! 操作符  
如果我就非得遇到空指针，强行用null来调用方法，那么就用双感叹号!!标记
```kotlin
a!!.length
```
6、安全的类型转换
```kotlin
val b = a as String  //把a进行类型转换，但有可能a不是String的子类对象，那么就会报类型转换异常
val b：String ？ = a as? String  //这样如果转换失败就返回null
```
7、等号操作符
```kotlin
= //赋值
==//判断值是否相等
===//判断内存地址是否相等
```
不仅可判断整形，字符串，对象都可以判断。这点和java很大不同。