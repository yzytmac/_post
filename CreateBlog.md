---
title: 搭建博客
date: 2016-10-15 14:23:50
tags: hexo博客
categories: 电脑技术
thumbnail: http://static.open-open.com/lib/uploadImg/20150620/20150620203424_361.png
---
# 从零教你搭建博客
## 安装git
1、Windows下就直接下载git客户端一直下一步  

2、Ubuntu就直接一条命令  

    sudo apt-get install git  
3、安装完成之后在命令行中输入git version回车，能显示git版本信息就算安装成功，接下来所有步骤都在git bash中进行了。
## 安装node.js
1、Windows依然是下载好node.js后一直下一步，最后要注意勾选上add to path添加到环境变量  

2、Ubuntu就直接输入两条命令  

    sudo apt-get install nodejs-legacy nodejs  
    sudo apt-get install npm
3、安装完毕输入node -v如果能得到版本信息就算安装成功  
## 安装Hexo
1、先创建一个文件夹用来存储我们的博客，就叫hexo文件夹吧
2、在git bash中cd到hexo路径下执行命令  

    npm i -g hexo
3、完毕后执行  

    hexo -v
4、如果得到版本信息代表安装成功
5、然后初始化博客，执行

    hexo init
## 在github中创建博客
1、打开自己的github，创建一个空项目，项目名叫 yzytmac.github.io  
- 注意，因为我的 github 是 www.github.com/yzytmac, 所以是这样起名字，你自己要吧yzytmac换成你自己的名字，".github.io"是固定格式，不能变  

2、关联git和github  
第一次使用git向github提交，需要先配置用户信息，执行命令 

    git config --global user.name "你的github名字"
    git config --global user.email "你的github绑定邮箱"
3、创建ssh  
    
    ssh-keygen -t rsa -C 你的邮箱
然后会让你指定生成id_rsa存放的位置，随你选，就选择它提示的位置就行  

4、github中添加生成的ssh  
github中-> 头像 -> settings -> SSH and GpG key -> New SSH key
然后用记事本打开刚才生成的id_rsa.pub，复制里面的内容，粘贴到github中来，title随便起  

5、一切都完成后在git 中执行  

    ssh -T git@github.com
如果提示成功，就代表ssh配置好了  
## 部署博客
1、在hexo中打开_config.yml,在里面配置好自己的github位置  

    deploy:
        type: git
        repo: https://github.com/YourgithubName/YourgithubName.github.io.git
        branch: master

2、在git中执行  

    hexo clean
    hexo generate
    hexo server
如果报错就执行  

    npm i hexo-server  
然后再重复一下上面三条命令  

3、如果成功，最下面会有提示 http://localhost:4000， 在浏览器中打开它，就可以看到自己的博客了  
4、部署到github中,执行  

    hexo deploy
就将项目上传到github中了，此时你就可以通过yzytmac.github.io这个网址访问你的博客了，当然yzytmac换成你自己的名字  
## 写博客
1、在hexo/source/_posts中创建一个后缀为md的文件，文件名就是文章名  

    hexo new "文章名" #新建文章
    hexo new page "page名" #新建页面
2、在文章的最上面写上  

    ---
    title: 文章标题
    date: 2018-01-26 14:23:50
    tags: 标签
    categories: 分类
    thumbnail: 缩略图
    ---
然后就开始写正文了。  
3、写完之后执行  

    hexo clean #简写hexo cl
    hexo generate #简写hexo g
    hexo server #简写hexo s
    hexo deploy #简写hexo d
    #常用组合
    hexo s -g
    hexo d -g
就可以在yzytmac.github.io看到你自己的新文章了。  
最后再推荐一篇文章写的挺好的[博客搭建](http://visugar.com/2017/05/04/20170504SetUpHexoBlog/)

## 联系我：
邮箱：yzytmac@163.com  
微信：  
![](https://raw.githubusercontent.com/yzytmac/yzytmac.github.io/master/medias/yzyweixin.png "微信二维码")  