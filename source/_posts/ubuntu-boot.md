---
title: 解决Ubuntu Boot分区占用100%问题
date: 2018-03-06 22:04:31
tags:
---
我的电脑装了双系统，win10+ubuntu，作为一个linux菜鸟，装了系统本想给自己一个学习的环境，结果大多时候还是选择windows开机，后来打开ubuntu的时候提示boot空间不足，想想莫非是装系统的时候分配的空间太小，现在后悔都来不及，难道又要再重装系统？后来百度了一下，才知道是因为boot分区内含有许多内核版本，内核版本会自动升级，而旧的版本不会自己卸载，所以导致boot分区的空间越来越小，需要我们手动进行卸载。

**查看系统正在使用的内核版本**
`$ uname -a`

**查看系统已经安装的内核版本**
`$ dpkg --get-selections | grep linux-image`

**删除旧的内核版本**
`$ sudo apt purge linux-image-extra-4.10.0-28-generic`

我在这一步的时候提示出错，报了个依赖的错误，就是删除不了，又百度了好多相关的资料，最后才找到相关的答案：

!()[/images/ubuntu/boot.png]
虽然英语不好，但是大概的意思还是看得懂的。
```bash
$ uname -r # 查看已安装的内核版本，注意不要去删除它
$ ls /boot # 这会列出所有安装的版本，选择一两个强制删除
$ sudo dpkg --force-all -P linux-image-3.13.0-32-generic # 强制删除
$ sudo apt-get install -f # 尝试修复依赖
$  sudo apt-get purge $(dpkg -l linux-{image,headers}-"[0-9]*" | awk '/ii/{print $2}' | grep -ve "$(uname -r | sed -r 's/-[a-z]+//')") # 最后执行清理旧版本命令
```
刚开始的时候只强制删除了一个版本，结果修复依赖的时候还是报错了，查了下boot又是100%，接着我一次多删除了几个版本，这才修复成功。

下面这三种方法也可以尝试一下，我接着按照如下半自动移除的方式，boot空间一下减小到25%。
!()[images/ubuntu/boot1.png]
