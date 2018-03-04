---
title: hexo实现多终端同步
date: 2018-03-04 15:30:45
categories:
- note
tags:
---
这两天学习如何用hexo与github搭建个人博客，博客是建好了，但是希望更进阶一点的知识，比如如何实现在不同的电脑也能实现博文的推送，网上查了很多相关的资料，自己对于git这个工具本身又不是太熟悉，所以索性又学一遍git基本的操作，同步的主要思路是*将整个项目的地址即hexo文件夹下的文件推送到hexo分支，多个终端只需要对hexo分支进行操作，修改后再推送到github，最后hexo布署时会自动推送到master分支。*

## 创建hexo分支
```bash
$ git init // 初始化本地仓库
$ git add . // 可以依次添加必要文件，这地方我暂时还搞不懂，所以直接添加所有文件
$ git commit -m "blog source hexo"
$ git checkout -b hexo // 添加并切换到分支
$ git remote add origin git＠github.com:yourname/youname.github.io.git //将本地与github项目对接
$ git push origin hexo // push到github项目的hexo分支
```

**使用第三方主题可能会导致主题无法push到远程仓库,原因在于你通过git clone下来的主题内含有.git文件夹，需要先将其删除再push，否则将会导致发布的博客是一片空白**

## 其它终端clone和push更新
将github上的hexo分支设置成默认仓库
其它电脑上clone远程仓库的hexo分支到本地
```bash
$ git clone git@github.com/yourname/yourname.github.io.git
```
进入本地仓库后执行`npm install`
依次执行`git add .`,`git commit -m "xxx"`,`git push origin hexo` 同步本地仓库到远程
最后部署博客`hexo d -g`

此后若在其它电脑上有做了新的推送，本地需先执行`git pull`同步远程修改到本地，然后再push。
参考：`https://righere.github.io/2016/10/10/install-hexo/`
