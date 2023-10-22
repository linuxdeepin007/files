---
title: LINUX服务器远程登陆后退出ssh，程序仍继续运行
date: 2023-05-03 
categories:
  - 编程电脑
  - LINUX
tags: 
   - 电视盒子
   - 远程登录
   - lINUX服务器
---
如何保证断开ssh后仍旧能保持更新进程的运行呢？有两种方法
<!-- more -->
​对Unix、Linux类服务器维护经常是通过ssh完成的，而有些操作执行时间较长，如：更新程序、文件备份、软件编译安装等。此时如果断开ssh连接的话，更新程序就会随之被中断。如何保证断开ssh后仍旧能保持更新进程的运行呢？有两种方法:

### 一、nohup

```
nohup 应用程序名 &
```

此后，如果你断开了ssh，程序依旧运行。

如果在运行后需要结束该进程，需要通过kill的方式。

### 二、screen

先通过yum install -y screen、apt-get install screen -y进行screen的安装。

#### （一）如何通过screen运行所需的进程

`screen`

然后按空格键或者回车后进入Screen会话，就可以运行用户所需要的程序了。

#### （二）运行所需进程后如何退出screen

运行用户所需的进程后，按下Ctrl+A，然后再按下d键，就可以切换回运行screen之前的主界面。

退出screen后，用户就可以在保证进程正常运行的情况下进行其他操作或者断开ssh连接。

#### （三）查看当前已经存在的screen会话

`screen -ls`

结果如下：
![](https://pic2.zhimg.com/v2-de99d693827ec639a401f9bd392d07a9_r.jpg)

#### （四）进入已有的screen会话

`screen -r 会话代号`

如：

```
screen -r 8858.pts-0.iZ28*****
```

可以进入当初用户执行进程所在的screen会话。
