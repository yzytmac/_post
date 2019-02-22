---
title: Gradle教程3---读懂Gradle
date: 2018-01-27 14:27:03
tags: Gradle
categories: Gradle教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517148693443&di=be20fb16f81144a2eafc668a8e35a626&imgtype=0&src=http%3A%2F%2Fstatic.open-open.com%2Flib%2FuploadImg%2F20160427%2F20160427151819_320.jpg
---
### groovy构建时并不是一开始就顺序执行build.groovy中的内容，而是分为两个阶段，配置阶段和执行阶段。在配置阶段会先读取Property、处理依赖等等。然后执行。

1、对于每一个Task，groovy都会在Project中创建一个同名的Property，所以我们可以将该Task当作Property来访问。  

2、groovy的数据类bean类似Scala和Kotlin，都会自动生成setter和getter方法  
```groovy
calss Person{
	private String name; //虽然是私有的，但是可以访问
}
```

3、大量的闭包  
```groovy
task A{
	Person p = new Person()
	p.config{
		name = "张三" //这里的name就是属于child的，因为c.delegate = child代码，所以对象就是child，整个代码块的环境都在child中了。
	}
	println p.child.name//出了代码块，所以就要写明调用对象
}
class Person{
	Child child = new Child()
	void config(Closure c){ //传一个闭包进来，也就是传一个代码块进来
		c.delegate = child //代理对象是child
		c.setResolveStrategy Closure.DELEGATE_FIRST //一些配置
		c() //执行闭包中的代码块
	}
}
class Child{
	private String name;
}
```






















