---
title: Kotlin教程8---委托与代理
date: 2018-01-28 14:35:03
tags: Kotlin
categories: Kotlin教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517214609323&di=40d0cb3d0cacdcc718de20dccb81fa6d&imgtype=0&src=http%3A%2F%2Fimgup01.sj88.com%2F2017-06%2F30%2F01%2F1498755765289_0.jpg
---
### 委托和代理的关系就是：A委托B做事，B就是A的代理人，B代理A做事

委托的前提是委托人和代理人必须实现同样的接口。  
委托的关键字是by。如：
```kotlin
interface IWash {
    fun wash()
}
class Son :IWash{
    override fun wash() {
        print("儿子洗碗")
    }
}
class Parent :IWash by Son()
```
这种情况下父可以亲不用实现洗碗的方法，而是委托给儿子去洗碗。  

父亲也可以实现洗碗方法，此时就会走爸爸的洗碗方法，而不会走儿子的洗碗方法，只有在爸爸的洗碗方法中在调用儿子的洗碗方法，儿子才会洗碗
```kotlin
class Parent :IWash by Son(){
    override fun wash() {
        Son().wash()
    }
}
```
