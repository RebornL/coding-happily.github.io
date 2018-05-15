---
title: 超简单的hexo+github page搭建博客
date: 2016-03-17 12:44:40
categories: 学习记录
tags: hexo
toc: true
---
目录

[ TOC ]
> 2018-05-15更新：增加hexo新增博客和编写的方式

## 1.在github上新建一个repo

**首先，先去[github](https://github.com/)申请好账号**
**创建一个仓库**
![hexo1](http://7xry59.com1.z0.glb.clouddn.com/hexo1.jpg)


**创建一个跟用户民一样的github仓库，每个用户只有一个自己的github page**
<!--more-->
![hexo2](http://7xry59.com1.z0.glb.clouddn.com/hexo2.jpg)


**然后，最后得到**
![hexo3](http://7xry59.com1.z0.glb.clouddn.com/hexo3.jpg)


**然后你可以尝试访问以下，[http://username.github.io](#),如果成功访问，这一部分就搞定。**


## 2.使用hexo搭建博客
**首先要先安装了nodejs和npm（Windows平台的安装包就包括了npm）**


**之后，先使用npm安装hexo-cli**
```
$ npm install hexo-cli -g
```


**在你自己新建目录里（我的是D:\Github\coding-happily.github.io）,打开git bash**
```
$ hexo init
$ npn install
```


**目录结构是这样的**
![hexo4](http://7xry59.com1.z0.glb.clouddn.com/hexo4.jpg)

```
$ hexo generate
$ hexo server
```


**打开地址：[http://localhost:4000/](http://localhost:4000/)，就能看到hexo搭建的博客**
![hexo5](http://7xry59.com1.z0.glb.clouddn.com/hexo5.jpg)

第二部分就准备好了

## 3.将hexo生成的代码部署到github上

**要将代码部署到github上，先安装hexo-deployer-git**
```
$ npm install hexo-deployer-git --save
```


**打开_config.yml文件，修改添加如下**
```
deploy:
  type: git
  repo: git@github.com:yourname/yourname.github.io.git
  branch: master
```


**配置完成后，就开始上传代码**
```
$ hexo clean
$ hexo d -g
```


**完成之后，可以尝试打开http://username.github.io/ 来查看效果如何**

## 4.配置域名部分

**前面基本完成了一个静态博客的搭建**

**关于域名部分配置，我主要想说的是，在域名解析的时候，填写的ip地址为github page提供，如果不知道，可以谷歌一下，一下就能查到**
**在[这个网址](https://help.github.com/articles/setting-up-an-apex-domain/)**
![hexo6](http://7xry59.com1.z0.glb.clouddn.com/hexo6.jpg)

推荐两个网站
*[史上最详细的Hexo博客搭建图文教程](https://xuanwo.org/2015/03/26/hexo-intor/)
<br />
*[如何搭建一个独立博客——简明Github Pages与Hexo教程](http://www.jianshu.com/p/05289a4bc8b2)


## 5.最后
我其实真的就是向上面那样撘完自己的博客，其实真的很简单的。
希望各位也能搭建自己的博客！！！

## 6.更新
```shell
hexo new "新的博客文章"
```
输入以上命令之后，会在本地文件夹source/_post/下出现**新的博客.md**，使用自己喜欢的markdown编辑器去编写博客文章。

使用以下命令发布博客文章。

```
hexo d -g
```

其他指令
```
hexo clean#这个命令一般用在你删除了md文件，重新生成
hexo generate
hexo deploy#这两个命令是以上命令的详细写法
```

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="http://music.163.com/outchain/player?type=2&id=26524326&auto=1&height=66"></iframe>