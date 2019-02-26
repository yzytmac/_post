---
title: 搭建SS/SSR教程
date: 2019-02-26 10:01:55
tags: [SS/SSR,科学上网,梯子,翻墙]
categories: 电脑技术
thumbnail: https://i1.wp.com/thatinterpreter.net/wp-content/uploads/2017/08/Shadowsocks.jpg?ssl=1
---

## 背景
由于国内网络环境特殊,导致国外很多优秀软件和网站无法使用,比如Google,YouTube,Dropbox等等,程序猿使用Google又是必备的,所以就需要借助梯子,但买别人的梯子一是速度慢,二是不安全(数据走别人服务器不安全,容易被请喝茶),所以就需要我们自己动手搭建自己的梯子了.这里只做学习交流,不要做违法乱纪的事,出事了与我无关.

## 准备
只需准备一个境外的vps服务器,综合价格,速度,方便,安全等诸多因素,我选择的是vutrl的 **[点我跳转去vutrl](https://www.vultr.com/?ref=7474996 "点我跳转")** ,从我这个链接进去新用户首充送10美金,支持支付宝,然后购买最3美金或5美金一个月的服务器,系统选centos就行了,地区选亚洲的国家最好,然后就进入搭建环节.

## 搭建
1. ssh到你的服务器  
```bash
ssh root@你服务器ip
```
2. 安装wget工具  
```bash
yum install wget
```
1. 安装脚本  
```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/yzytmac/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```
4. 配置  
当看到"请输入数字 [1-15]:"时就代表安装完成,可以开始配置了:  
输入1回车->端口号默认2333,不修改就直接回车->设置密码后回车->加密方式直接回车->协议直接回车->是否兼容回车->混淆协议直接回车->设备限制无限直接回车->速度无限直接回车->端口无限直接回车->然后就是等待...->然后就配置完了,会打印如下信息,自己保存好
```
 ShadowsocksR账号 配置信息：

 I  P	    : xx.xx.xx.xx
 端口	    : 2333
 密码	    : doub.io
 加密	    : aes-128-ctr
 协议	    : auth_sha1_v4_compatible
 混淆	    : plain
 设备数限制 : 0(无限)
 单线程限速 : 0 KB/S
 端口总限速 : 0 KB/S
 SS    链接 : ss://YWVzLTOC1jdHI6ZG91Yi50AxMTMuOTIuMzUjQ0OjIzMzM
 SS  二维码 : http://doub.pw/qr/qr.php?text=ss://YWVzLdHI6ZG91Yi5pb0AxMTMuOTIuMzUuMjQ0OjIzMzM
 SSR   链接 : ssr://MTEzLjkyLjM1LjI0NDoyMzMzOmF1dGhfc2hhZXMtMTI4LWN0cjpwbGFpbjpaRzkxWWk1cGJ3
 SSR 二维码 : http://doub.pw/qr/qr.php?text=ssr://MTEzLjjI0NDoyMzMzOmFc2hhMV92hZXMtMTWN0cjpwbGFpbjpaRzkxWWk1cGJ3
```

## 使用
接下来就可以在手机,平板,电脑,路由器上使用了.在设备上安装ss客户端或ssr客户端,然后复制上面的SS链接或SSR链接,将链接导入到客户端中,然后连接,此时你的设备就可以访问墙外的世界了.打开Google或YouTube试试,如果有问题仔细看看步骤是不是都对,如果还是不行可以在博客右上角联系我.

## 声明
再次声明,此贴只为学习交流使用,不要做违法乱纪,危害国家安全的事情,如果此贴不合规,请联系我删帖!!
