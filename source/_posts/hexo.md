---
title: hexo简明教程
date: 2018-01-27 06:20:37
toc: true  
tags:
- hexo
categories:
- note
---
> Hexo - 快速、简洁且高效的博客框架，支持Markdown
GitHub Page 提供300M免费空间
hexo的安装需要依赖Node.js,发布依赖Git
在本地编辑，生成静态文件，通过git发布到GitHub

## 安装依赖

**Node.js:** [下载地址](https://nodejs.org/en/download "nodejs")
**Git:** [下载地址](https://git-scm.com/downloads "git")
### 设置git账户

```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
### 查看设置信息

```bash
$ git config user.name
$ git config --list
```
或查看~/.gitconfig文件

### 生成密钥对

```bash
$ ssh-keygen -t rsa -C "youremail@example.com"
```
在~/.ssh目录内有id_rsa(私钥)和id_rsa.pub(公钥)，

**安装Hexo**

```bash
$ cd you-blog-path
$ npm install -g hexo-cli
$ hexo init
```
## 设置GitHub

将上面生成的公钥加入到GitHub中
新建仓库，名称为：yourname.github.io **此处yourname必须为GitHub账户名**

## 发布网站

### 修改配置文件

```text _config.yml
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master
```
### 执行命令

在博客目录下分别执行Git命令
```bash
$ hexo clean
$ hexo generate
$ hexo deploy
```
### 查看站点
在浏览器中输入`http://yourgithubname.github.io` 查看站点

## 绑定个人域名

在`you-blog/source/`目录下创建CNAME文件，添加上域名
比如本站添加为`www.akindman.com`
设置DNS记录
![](/images/20180126232433.png)

