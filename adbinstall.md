---
title: 一键安装并打开APK脚本
date: 2019-02-28 15:12:30
tags: [shell,adb,android]
categories: Android
thumbnail: https://www.xda-developers.com/files/2018/04/ADB.png
---
## 使用场景
有一个demo.apk的安装包,需要安装到手机后并启动它,最low的方式就是把apk拷到手机,然后找到他,然后点击安装,最后在桌面找到它,点击图标启动.这样效率太低了.所以我写了这个一键安装并打开APK脚本,只需一行命令就完成上述操作.
```shell
install demo.apk
```

## 原理
1.先使用aapt命令获取安装包的信息  
2.解析出包名,主页面名,然后构造出componentName  
3.将demo.apk用adb推到手机中  
4.用pm安装demo.apk  
5.根据之前构造出的componentName,用am来进行启动  
**注意:**需将adb和aapt等提前配置到环境变量中去!  
## 编写脚本
1.创建一个空文件,名字随意,这里就起名install  
2.复制下面脚本到文件中  
3.为脚本添加执行权限chmod +x install  
4.把install添加到环境变量中  
```shell
#!/bin/bash
str=$(aapt dump badging $1 |grep launchable-activity)
# launchable-activity: name='com.oppo.market.activity.MainActivity' label='' icon=''
str=${str#*\'}
activity=${str%%\'*}
echo "activity->$activity"

str=$(aapt dump badging $1 |grep package)
#package: name='com.oppo.market' versionCode='6002' versionName='6.0.0' platformBuildVersionName='7.1.1'
str=${str#*\'}
pkg=${str%%\'*}
echo "pkg->$pkg"
cn="$pkg/$activity"
echo "cn->$cn"

#adb install -r $1
adb push $1 /data/local/tmp/tmp.apk
echo "$1 is installing..."
adb shell pm install -r /data/local/tmp/tmp.apk
adb shell am start -n $cn -a android.intent.action.MAIN -c android.intent.category.LAUNCHER
```

## 使用
```shell
install demo.apk
```
