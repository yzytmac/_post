---
title: Gradle教程2---task的创建和配置
date: 2018-01-27 14:26:03
tags: Gradle
categories: Gradle教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517148693443&di=be20fb16f81144a2eafc668a8e35a626&imgtype=0&src=http%3A%2F%2Fstatic.open-open.com%2Flib%2FuploadImg%2F20160427%2F20160427151819_320.jpg
---
### groovy的Project从本质上来说就是一个task的容器，一个task和Ant中的target一样，是一个逻辑执行单元。所有的task都存放在Project的taskContainer中。tasks就是管理这个容器的一个task，tasks.size()就可以得到容器中有多少个task。

1、利用groovy的DSL语言创建  
```groovy
task task1{xxx} //创建一个简单的task
task task2 <<{xxx} //在最后面追加代码，和task3意义一样
task task3{
	doLast{ xxx} //在最后面追加代码
}
task task4{
	doFirst{xxx} //在最前面加入代码
}
```

2、通过tasks的create方法像容器中添加task  
```groovy
tasks.create(name: 'task5')<<{xxx}
```
name后面的task5就是新task的名字  

3、配置task  

每个task还包含一些属性Property，默认的有logger、description等，一些特定的task还有特定的属性，如Copy的task还包含from和to  
①在创建的时候进行配置
```groovy
task task6<<{
	description = "我是task6"
	xxx
}
```
②闭包的方式创建  
```groovy
task task7<<{xxx}
task7{ description = "我是task7"} //顺序不影响，因为会先加载配置，然后才真正的执行
```
③通过configure来进行配置  
```groovy
task task8<<{xxx}
task8.configure{
	description = "我是task8"
}
```
实际上所有的配置在内部都是调用的configure进行配置的























