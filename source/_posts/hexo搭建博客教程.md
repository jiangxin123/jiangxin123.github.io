---
title: hexo搭建博客教程
date: 2017-08-30 11:25:22
tags:
---

![illustration](http://photo.foter.com/photos/398/creative-brush-notebook.jpg)
### 介绍
本文旨在帮助没有IT背景的同学着手搭建一个酷炫的个人博客网站，基于Windows平台

<!--more-->

### 准备
注册[GitHub](http://baike.baidu.com/item/GitHub)账号，了解一点有关Github的知识。

### 开始
假设我们已经有了一个github账号，那么开始准备环境

1.安装Git客户端 
[download git](https://www.git-scm.com/download/)
下载好git安装包之后按照一般程序安装步骤安装，有选项则选择默认配置，一路next

2.安装Node.js
[download node.js](https://nodejs.org/dist/v6.10.2/node-v6.10.2-x64.msi)
下载好node.js安装包之后按照一般程序安装步骤安装，有选项则选择默认配置，一路next
具体安装细节可参考http://www.runoob.com/nodejs/nodejs-install-setup.html

3.安装Notepad++
[download notepad++](https://notepad-plus-plus.org/repository/7.x/7.3.3/npp.7.3.3.Installer.exe)
安装步骤同上

### 建立仓库
这时我们已经安装好了相关的软件，接下来初始化配置一个存放博客资源的GitHub仓库

1.登录GitHub官网，新建后缀名为`.github.io`的仓库

点击页面右上角加号，选择`New resposity`

![new repo-1](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/new%20repo-1.png)



进入仓库创建页面
在`Respository name`下填写你的博客仓库名，切记以`.github.io`为后缀名，`Description`一栏可以随便填写一些描述文字，空着也行

![new repo-2](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/new%20repo-2.png)



完成博客仓库的创建之后，将跳转到如下界面

![repo done](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/repo%20done.png)



2.给仓库开启GitHub-pages功能
点击博客仓库首页右上侧的`Settings`，跳转到仓库的设置界面，向下拖动页面到`GitHub Pages`一栏

![Github-pages](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/Github-pages.png)

点击`Automatic page generator`，Github将会自动替你创建出一个github-pages的页面。 如果配置一切正确，那么大约15分钟之后，yourname.github.io这个网址就可以正常访问了。

3.添加本机ssh密钥到github

在桌面上右击鼠标，选择`Git GUI Here`
![git gui](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/git%20gui.png)



进入git gui界面，选择`Help`-`Show SSH Key`![git gui-2](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/git%20gui-2.png)



点击`Generate Key`生成ssh key，出现如图一串密钥，全部复制
![generate-ssh-key](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/generate-ssh-key.png)



登录github，点击头像选择`Settings`

![ssh-setting](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/ssh-setting.png)

进入设置页面选择`SSH and GPG keys`

![ssh setting2](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/ssh%20setting2.png)

进入SSH设置页面，点击右上角绿色按钮`New SSH key`，然后把复制的ssh key密钥粘贴到`Key`文本框里，`Title`一栏随便起个名字
![add ssh key](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/add%20ssh%20key.png)
最后点击`Add SSH key`
到了这里，GitHub一侧的配置工作全部完成



### Hexo搭建

1.安装Hexo
创建一个文件夹存放hexo博客资源，进入文件夹右击鼠标选择`Git Bash Here`，将弹出一个黑乎乎的终端窗口，之后我们将在这个窗口内敲一些操作命令，我们暂时不用去了解终端命令行，只需照着打字即可

![new folder](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/new%20folder.png)



在终端中输入`npm install hexo-cli -g`，这条命令用来安装hexo-cli
安装完成将会看到下图（忽略warning）

![install hexo-1](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/install%20hexo-1.png)



输入`nmp install hexo --save`，安装完成后屏幕里将输出大堆信息提示
检查hexo是否正确安装，输入`hexo -v`，下图为正确安装的提示信息

![hexo-v](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/hexo-v.PNG)



2.初始化Hexo
输入`hexo init`进行初始化
安装hexo的相关npm依赖模块：

```bash
npm install
```


3.测试体验hexo博客
分别依次输入以下命令

```bash
hexo g
hexo s
```
出现如下提示
![run hexo](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/run%20hexo.PNG)



在浏览器中打开`http://localhost:4000`，将打开hexo站点，主题是hexo默认的

![hexo homepage](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/hexo%20homepage.png)

到了这一步，hexo的基本配置就完成了

3.把hexo部署到github-pages上
参考[Hexo 官方配置文档](https://hexo.io/zh-cn/docs/configuration.html)，通过修改hexo主配置文件`_config.yml`来部署hexo
用Notepad++打开`_config.yml`，拖到文件最后，有如下配置语句
```bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type:
```
修改如下
```bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:  
  type: git
  repository: git@github.com:yourname/yourname.github.io.git
  branch: master
```
(注：yourname是你的github用户名)

保存后，在当前文件夹打开Git Bash Here
安装hexo的git依赖模块，出现弹窗则输入github账号和密码

```bash
npm install hexo-deployer-git --save
```
发布hexo到github-pages
```bash
hexo d -g
```
### 感受hexo博客发布
1.新建一篇博客，hexo命令语法课参考[Hexo指令官方文档](https://hexo.io/zh-cn/docs/commands.html)
```bash
hexo n "这是第一篇测试博客"
```
![create blog](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/create%20blog.PNG)
这条命令将在`source/_posts`目录下新建一个`.md`后缀的markdown文件，这就是你的博客文章的载体，你需要了解[markdown](http://wowubuntu.com/markdown/)语法，使用markdown来编写你的博客

2.编写博客

用Notepad++打开`这是第一篇测试博客.md`，编写文章内容，最后保存

![edit blog](https://github.com/Zhiwei1996/Zhiwei1996.github.io/raw/master/images/edit%20blog.PNG)

发布文章

```bash
hexo d -g
```

### 换个漂亮的主题
### 建立git分支给博客做备份
