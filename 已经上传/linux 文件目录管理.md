---
title: LINUX文件目录管理
date: 2022-06-16 
categories:
<<<<<<< HEAD
  - 编程电脑
=======
  - 电脑编程
>>>>>>> 674a6daf68e3f3f257715aba490f2170e5a61265
  - LINUX
tags: 
   - LINUX
   - 文件目录管理
   - 命令行	
---
linux首先建立一系列空目录，然后将文件挂载到目录中。主要介绍了目录内容和几个重要的文件管理命令。
<!-- more -->

<<<<<<< HEAD
## 一、linux 主要目录及其内容
=======
# 一、linux 主要目录及其内容
>>>>>>> 674a6daf68e3f3f257715aba490f2170e5a61265

|目录|内容|
|:----:|:----:|
|/bin|常用命令|
|/boot|内核与启动文件|
|/dev|各种设备文件|
|/etc|系统软件的启动和配置|
|/home|用户目录|
|/lib|C编译器的库|
|/media|可移动介质安装点|
|/opt|可选的软件安装包|
|/proc|进程的镜像|
|/root|超级用户的主目录|
|/sbin|和系统操作有关的命令|
|/tmp|临时文件存放点|
|/usr|非系统的程序和命令|
|/var|系统专用的数据和配置文件|

<<<<<<< HEAD
## 二、共享文件实例
=======
# 二、共享文件实例
>>>>>>> 674a6daf68e3f3f257715aba490f2170e5a61265
需求：新建一个名称是happygroup的用户组，添加user1、 user2和user3三个用户，设置工作目录为sharehappy。设置user1为管理者，并且除了本用户组外，其他人无法修改文件。

```bash
# 新建一个名称为happygroup的用户组，并创建用户
linux@linux-ThinkCentre-E75:/home$ sudo groupadd happygroup
# 新建三个用户归入happygroup用户组，并设置密码为123
inux@linux-ThinkCentre-E75:/home$ sudo useradd -G happygroup user1
linux@linux-ThinkCentre-E75:/home$ sudo passwd user1
新的 密码： 
重新输入新的 密码： 
passwd：已成功更新密码
linux@linux-ThinkCentre-E75:/home$ sudo useradd -G happygroup user2
linux@linux-ThinkCentre-E75:/home$ sudo useradd -G happygroup user3
linux@linux-ThinkCentre-E75:/home$ sudo passwd user2
新的 密码： 
重新输入新的 密码： 
passwd：已成功更新密码
linux@linux-ThinkCentre-E75:/home$ sudo passwd user3
新的 密码： 
重新输入新的 密码： 
passwd：已成功更新密码
# 在home目录下新建名为sharehappy的文件夹
linux@linux-ThinkCentre-E75:/home$ sudo mkdir sharehappy
# 将sharehappy文件夹的权限交给happygroup
linux@linux-ThinkCentre-E75:/home$ sudo chgrp happygroup  sharehappy/
# 增加happygroup组对sharehappy文件目录的读写执行权限
linux@linux-ThinkCentre-E75:/home$ sudo chmod g+rwx sharehappy/
# 撤销其他用户对该目录的读写执行权限
linux@linux-ThinkCentre-E75:/home$ sudo chmod o-rwx sharehappy/
# 把sharehappy目录的所有者更改为user1
linux@linux-ThinkCentre-E75:/home$ sudo chown user1 sharehappy/

```
<<<<<<< HEAD
## 三、创建文件命令
=======
# 三、创建文件命令
>>>>>>> 674a6daf68e3f3f257715aba490f2170e5a61265
touch命令可以新建一个空文件，当某个程序需要一个文件无法启动，而这个文件实际上并不重要，可以通过新建一个空文件来骗过程序。
touch的另一个用途是可以更新文件的时间等信息，而对内容不做更改。
