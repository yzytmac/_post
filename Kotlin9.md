---
title: Kotlin教程9---let、apply等区别
date: 2018-01-28 14:36:03
tags: Kotlin
categories: Kotlin教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517214609323&di=40d0cb3d0cacdcc718de20dccb81fa6d&imgtype=0&src=http%3A%2F%2Fimgup01.sj88.com%2F2017-06%2F30%2F01%2F1498755765289_0.jpg
---
### let、apply、with、run、also的区别  
通过运行以下代码来展示他们的区别，主要在于有无返回值、this和it关键字来代替本身等等
```kotlin
fun main(args: Array<String>) {
    println("------------run-------------------")
    //public inline fun <T, R> T.run(block: T.() -> R): R = block()
    val a = "yang".run {
        println(this)
    }
    println("a:$a")

    println("------------let-------------------")
    //public inline fun <T, R> T.let(block: (T) -> R): R = block(this)
    val b = "yang".let {
        println(it)
    }
    println("b:$b")

    println("-------------apply------------------")
    //public inline fun <T> T.apply(block: T.() -> Unit): T { block(); return this }
    val c = "yang".apply {
        println(this)
    }
    println("c:$c")

    println("-------------also------------------")
    //public inline fun <T> T.also(block: (T) -> Unit): T { block(this); return this }
    val d = "yang".also {
        println(it)
    }
    println("d:$d")

    println("---------------with----------------")
    //public inline fun <T, R> with(receiver: T, block: T.() -> R): R = receiver.block()
    val e = with("yang"){
        println(this)
    }
    println("e:$e")
}
```
