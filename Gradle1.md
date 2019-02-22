---
title: Gradle教程1---快速入门
date: 2018-01-27 14:25:03
tags: Gradle
categories: Gradle教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517148693443&di=be20fb16f81144a2eafc668a8e35a626&imgtype=0&src=http%3A%2F%2Fstatic.open-open.com%2Flib%2FuploadImg%2F20160427%2F20160427151819_320.jpg
---
### groovy是构建工具，是用groovy语言写的。
1、环境搭建  

下载gradle，将bin目录配置到环境变量中，gradle -v出现版本信息就说明配置成功  
2、hello gradle  

任意文件夹下新建build.gradle文件，然后写上第一个task  
```groovy
task hello << {
	println "hello gradle"
}
```
然后在build.gradle目录下执行gradle hello，命令行中就会打印出hell gradle  
这里“<<”表示向任务hello中加入一段执行代码，就是groovy代码。groovy给我们提供了一整套DSL语言，所以看起来脱离了groovy语法，其实内部还是groovy实现的，这点不要搞错了。
“<<”是一种快捷方式，代表的语句是doLast，如：  
```groovy
task hello  {
	doLast{
		println "hello gradle"
	}
}
```
甚至最简单的  
```groovy
task hello{ println "hello gradle"}
```
3、task类型  

像上面的task就是gradle中的一个默认类型DefaultTask的对象，我们可以声明其他的类型，甚至自定义类型。如用Copy类型：  
```groovy
task cofyFile(type: Copy){
	from: 'fileA'
	to: 'fileB'
}
```
声明一个类型为Copy的task，作用就是把文件(夹)A中的内容拷贝到B  

4、task之间的依赖  

task之间也是可以依赖的  
```groovy
task taskA{
	println "wo shi A"
}
task taskB(dependsOn: A){
	println "wo shi B"
}
```
比如执行gradle taskB，因为B依赖A，所以会先执行A，再执行B  
还可以直接声明谁依赖谁：  
```groovy
task C{xxx}
C.dependsOn A
```
而不用在创建task的时候声明  

5、自带的task  

gradle默认自带几个常用task供我们使用。如：tasks、properties、help、projects等  
当执行gradle tasks时：会列出当前build.gradle中所有的task，当然就包含我们前面的hellogroovy、taskA、taskB以及系统自带的这些个默认的task。dependencies用于显示Project的依赖信息，projects用于显示所有Project，包括根Project和子Project，properties则用于显示一个Project所包含的所有Property。这里就不一一试了。























