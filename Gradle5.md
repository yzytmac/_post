---
title: Gradle教程5---依赖管理
date: 2018-01-27 14:29:03
tags: Gradle
categories: Gradle教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517148693443&di=be20fb16f81144a2eafc668a8e35a626&imgtype=0&src=http%3A%2F%2Fstatic.open-open.com%2Flib%2FuploadImg%2F20160427%2F20160427151819_320.jpg
---
1、repositories()方法用来声明依赖的远程仓库，如  
```groovy
repositories {
	mavenCentral()
    jcenter()
    maven { url "https://jitpack.io" }
}
```

2、自己为依赖分组，如正式版依赖release组的，测试版依赖debug组
```groovy
configurations{
	myRelease //这些都是自定义的，像compile、testCompile这些是java或android插件中已经定义好的
	myDebug
}
```
3、依赖  
```groovy
dependencies{
	myRelease 'com.qiniu:qiniu-android-sdk:7.2.+'
	myDebug 'com.qiniu:qiniu-android-sdk:7.0.0'
	compile 'com.qiniu:qiniu-android-sdk:7.2.+' //android自带用的是compile
	testCompile 'junit:junit:4.12' //android的测试依赖
	myRelease project(':ProjectB') //对其他的Project进行依赖
	compile fileTree(dir: 'libs' ， include: ['*.jar']) //依赖本地文件夹中的jar文件，dir来指定目录，include用来指定要依赖的文件格式，可以是单个或数组的形式
	compile files('spring-core.jar', 'spring-aap.jar') //依赖具体摸个jar文件
}
```
依赖里面的格式是组名+项目名+版本号，所以我们可以拆开来依赖，就完全是gradle的语法,如：
```groovy
myRelease group:'com.qiniu', name:'qiniu-android-sdk', version:'7.2.+'
```
用逗号和冒号隔开  

4、依赖aar  
```groovy
repositories{
	flatDir{
		dirs 'aars' //在app下创建一个文件夹，名字随意就叫aars吧，当然也可以不创建，直接用libs行，但要在这里声明aar放在哪个文件夹下
	}
}
compile (name:'aarName',ext:'aar') //依赖该aar，写上名字和后缀格式
```
5、依赖so  

在main下创建jniLibs文件夹，将so文件放进去即可自动依赖  

6、依赖moudel  
```groovy
compile project(':moudelName')
```




































































