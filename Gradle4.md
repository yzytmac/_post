---
title: Gradle教程4---自定义Property
date: 2018-01-27 14:28:03
tags: Gradle
categories: Gradle教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517148693443&di=be20fb16f81144a2eafc668a8e35a626&imgtype=0&src=http%3A%2F%2Fstatic.open-open.com%2Flib%2FuploadImg%2F20160427%2F20160427151819_320.jpg
---
Gradle默认为Project创建了很多Property，常用的有：
- project ：Project本身
- name： Project的名字
- version： Project的版本信息
- path： Project的绝对路径
- description： Project的描述信息
- buildDir：Project构建后存放的目录

新建一个build.gradle文件  
```groovy
version = 'this is version info'  //Project的version
description = 'this is description'  //Project的description
task show<<{
	println version
	println project.description //因为每个task也有description，所以要加上project调用的才是上面定义的
}
```
上面的version和description都是使用Project自带的Property，如果我们自定义的就不可以直接这样写  

1、在build.gradle中自定义Property  
```groovy
ext.java_version = "1.9.0"
```
或用闭包的形式
```groovy
ext{
	kotlin_version = '1.1.4'
}
task show{
	println java_version
	println kotlin_version
}
```
事实上任何实现了ExtentionAware的对象都可以通过这种形式进行添加额外的porperty，Project、和Task都实现了这个接口，所以可以用这种形式添加

2、通过命令行参数进行添加Property
```groovy
task show{ println yzy} //yzy并没有定义
```
在命令行输入gradle show时加上参数
```groovy
gradle -P yzy=‘i am yangzhneyu’ show
```

3、通过jvm系统参数进行设置
```groovy
gradle -Dorg.gradle.project.yzy="i am yangzhneyu" show
```
4、环境变量的形式
```groovy
export ORG_GRADLE_PROJECT_yzy="i am yangzhneyu"
```
然后执行gradle show





































































