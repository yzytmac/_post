---
title: Kotlin教程7---闭包
date: 2018-01-28 14:34:03
tags: Kotlin
categories: Kotlin教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517214609323&di=40d0cb3d0cacdcc718de20dccb81fa6d&imgtype=0&src=http%3A%2F%2Fimgup01.sj88.com%2F2017-06%2F30%2F01%2F1498755765289_0.jpg
---
### 1、什么是闭包？？？
闭包是一个概念，它描述了函数执行完毕内存释放后，依然内存驻留的一个现象，只要把握这个核心概念，闭包就不难理解了。

### 2、闭包的作用
实际上是就是闭包延长变量的生命周期。通常函数的作用域即变量会在函数执行结束后被销毁，但当函数返回一个闭包，只要闭包不被释放，整条作用域链都会占用内存。

### 3、举例说明
普通非闭包：
```kotlin
fun test(){
    var i = 3
    println(i++)
}
fun main(args:Array<String>){
    test()
    test()
    test()
}
```
这种情况就是普通的函数调用，会打印三个3.为什么会这样呢？因为函数执行完成之后生命周期就结束了，就会被GC回收，所以每次的 i 都是一个新的变量，都是从3开始的。

闭包的形式：
```kotlin
fun test():()->Unit{
    var i = 3
    return fun(){
        print(i++)
    }
}
fun main(args:Array<String>){
    var t = test()
    t()
    t()
    t()
}
```
这样执行后的结果就是3 4 5 。为什么呢？  
来分析下。在kotlin中既是面向对象，又是面向函数，所以类和函数都是一等公民。而java中类是一等公民，属性和方法是二等公民。  
这有什么区别呢？  
就是一等公民中可以再定义方法，而二等公民中是不可以。这点很重要，正如我们知道的全局作用域、局部作用域。。。一样，全局不能访问局部，但局部可以访问全局。如果在最外层能拿到最内层的引用，通过最内层的引用我们就能访问所有，这个概念就叫做闭包。如例子，main的大括号算最外层，test的大括号算第二层，return的大括号算最内层，我们把最内层返回给最外层，在最外层执行返回的函数。
那么来分析下为什么是3 4 5 的呢？当执行t()后test()的生命周期就已经结束了，应该被GC，但是mian中持有最内层的引用t，骨test不能被GC，而t有持有i的引用，故内存的中i就等于4，当再次执行t()的时候就会直接将4打印出来，然后周而复始。终极原因就是最外层引用了最内层，最内层引用了的二层，只要最外层还持有引用第二层和最内层就不会被GC从而延长了函数的生命周期。并且也使函数具有了状态。其实对象之所以有状态就是因为类被一直持有引用的时候不会被GC，有了很长的生命周期，所以才会有状态的，所以只要生命周期够长，就会有状态，这也是闭包最重要的特性。  

### 4、为什么Kotlin有闭包而java没有呢？  
因为kotlin中方法也是一等公民，所以方法中可以定义方法。而java中的方法是二等公民，里面不能定义方法，所以就更不能返回出一个带中间层引用的函数出来。

由于kotlin也是面向函数、面向属性的，所以一个文件中可以直接是一个方法或一个属性。不像java那样，一个文件中必须是类，方法和属性必须在类中。如：直接创建一个kt文件，随便命名，里面直接写
```kotlin
const val A = "apple"
```
在其他文件中就可以直接访问常量A了。这也是kotlin的强大之处。

### 5、闭包的一个实际使用场景，就是功能上和接口回掉一样  
```kotlin
class MainActivity : Activity() {
    var tv_pro: TextView? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        tv_pro = findViewById(R.id.tv_pro)
    }

    fun onClick(button: View) {
        Thread {
            //download(tv_pro!!).invoke()
            //或download(tv_pro!!)()
            //或
            var complete = download(tv_pro!!)
            complete()

        }.start()
    }

    fun download(tv: TextView): () -> Unit {
        for (i in 0..10) {
            SystemClock.sleep(500)
            if (i == 10) {
                return fun() {
                    this@MainActivity.runOnUiThread {
                        tv.text = "下载完成"
                    }
                }
            } else {
                this@MainActivity.runOnUiThread {
                    tv.text = "下载进度：$i"
                }
            }
        }
        return fun() {}
    }
}
```
这个是典型的利用闭包的特性完成了接口回掉 的功能



















