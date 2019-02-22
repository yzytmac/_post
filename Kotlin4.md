---
title: Kotlin教程4---类型转换
date: 2018-01-28 14:31:03
tags: Kotlin
categories: Kotlin教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517214609323&di=40d0cb3d0cacdcc718de20dccb81fa6d&imgtype=0&src=http%3A%2F%2Fimgup01.sj88.com%2F2017-06%2F30%2F01%2F1498755765289_0.jpg
---
智能类型转换：
```kotlin
val a:Any = xxx
if (a is String){
//在大括号范围内a自动转换成String类型，就可以调用String中的方法
print(a.length)
}
//当出了大括号就恢复成Any类型
print("a is any")
```
不仅如此，还有更智能的
```kotlin
if(a !is String){ 
    //大括号中的a不是String类型
}
//出了大括号a就是String类型
print(a.length)
```
`||` 右侧的 x 自动转换为字符串
```kotlin
if (x !is String || x.length == 0) return
```
`&&` 右侧的 x 自动转换为字符串
```kotlin
if (x is String && x.length > 0) {
    print(x.length) // x 自动转换为字符串
}
```
强制类型转换
```kotlin
val b = a as String  //把a强转成String类型
val b = a as? String  //安全的把a转换成String
```