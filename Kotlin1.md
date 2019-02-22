---
title: Kotlin教程1---基础语法
date: 2018-01-28 14:29:03
tags: Kotlin
categories: Kotlin教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517214609323&di=40d0cb3d0cacdcc718de20dccb81fa6d&imgtype=0&src=http%3A%2F%2Fimgup01.sj88.com%2F2017-06%2F30%2F01%2F1498755765289_0.jpg
---
1、数据类型、注意全是大写字母开头
```kotlin
Byte //8位
Short //16位
Int //32位
Long //64位
Float //32位
Double //64位
```

2、定义变量和常量(和scala一样)
```kotlin
//var定义变量
var a:Int = 1 
var b:String = "haha"
//val定义常量
var a2:Int = 1 
var b2:String = "haha"
```
3、定义函数(和scala一样只是def变成了fun，不加=)
```kotlin
fun funName(x:String,b:Int):Unit{
	//todo
}
```
- 注意：scala中有=代表有返回值，无=代表无返回值。
    而Kotlin中有=代表为=前的方法名赋值一个方法体。所以创建函数的时候不要轻易使用=，除非方法体是一句表达式。也就是说有等号就无大括号、无return可以省略返回值类型；无等号就必须有大括号、可以有return，有了return就必须有返回值类型，不能省略，省略相当于返回类型是Unit，这个和scala是不同的如：
	```kotlin
	fun add(x:Int,y:Int)=x+y
	fun add(x:Int,y:Int):Int{return x+y}
	```

4、函数的中缀表示法  
- 他们是某类的成员函数或扩展函数
- 他们有且只有一个参数
- 他们用 infix 关键字标注如：
	```kotlin
	class A{
		infix fun haha(content:String){....}  //这是成员函数
	}
	fun main(args:Array<String>){
		//这是扩展函数
		infix fun A.heihei(content:String){
			//todo
		}  
		val a = A()
		a.haha("yzy")
		a.heihei("yzy")
		a haha "yzy"
		a heihei "yzy"
	}
	```

- 默认参数。  
	在方法（包括构造方法）的参数列表定义的时候就可以初始化赋值。调用的时候可以依次传值，也可以不传直接使用默认值。但是调用java的方法时不可以这样。如：
	```kotlin
	fun haha(name:String = "yzy" ,age:Int){}
	```
	调用
	```kotlin
	haha(age = 18)
	//或
	haha(18)
	//或
	haha("wyq",18)
	```

5、异常捕获（和java的写法一样）
```kotlin
try {
    //有异常的代码部分
}catch (e:Exception){
    //todo    
}
```

6、尾递归（尾部递归）  
就是再函数体的尾部进行函数的再调用，切记是尾部。然后用 **tailrec**关键字修饰。这才叫做尾递归。不然就还是普通的递归.如：
```kotlin
tailrec fun findFixPoint(x: Double = 1.0): Double 
= if (x == Math.cos(x)) x else findFixPoint(Math.cos(x))
//代码的意思就是如果x=cos(x),那么函数返回值就是x，否则就将cos（x）的值传入函数继续调用执行
```




































































