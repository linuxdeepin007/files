---
title: Linux入门005_源代码编译软件
date: 2022-07-08
categories:
   - 编程电脑
   - Linux
tags: 
   - 编译
   - 软件
   - Linux 
---
尽管各类软件包管理工具已经很完美地解决了Linux下软件问题，但有些时候不得不求助于最原始的方法。
<!-- more -->
以多媒体播放软件Mplayer为例，讲解源代码编译。虽然不同的Linux发行版本有些许差异，但基本的思路是一致的。

## 一、为什么要从源代码编译

- 一些开发商并没有提供二进制的软件包，或者只为特定版本提供了安装包，使用源代码编译是其唯一选择。
- 鉴于Linux的开放性，一些企业或者个人有定制化需求，这些修改了的软件必须重新编译。
- 源代码编译软件，可以最大限度地控制软件，例如软件安装的位置以及某些功能的禁用。

## 二、下载和解压软件包

mplayer同时支持mcos、windows和Linux。

### （一）下载mplayer

```bash
http://www.mplayerhq.hu/MPlayer/releases/MPlayer-1.5.tar.xz
```

### （二）解压缩mplayer

## 三、配置软件

Linux所有的软件都是用configure 这个脚本配置以源代码形式发布的软件，configure依据用户提供的参数生产makefile文件。

configure脚本几乎都有 --prefix选项，用于指定软件安装位置。但是不同软件有不同的设置，区别很大，需要借助软件的安装文档（README/INSTALL）查看。

> 通常把软件安装在local目录

```bash
./configure
./configure --prefix=/usr/local/games/foobillard
```

大部分时候，此时会报错，根据内容修改补充解决报错，指导成功满足安装环境为止。

## 四、编译源代码

`make` 是一种高级编译工具，他可以依据Makefile中的规则调用合适的编译器编译源代码。

通过查看帮助文件我们可以看到

```bash
make
```

## 五、安装软件到系统

使用make命令编译完源代码之后，可以使用 `make install` 命令执行安装命令。

至此，mplayer主程序就安装完成了。此时还需要查看README安装帮助文件

```bash
make install

```

## 六、安装出错的处理

使用源代码安装软件非常容易出错，对照帮助文档和出错信息可以对问题进行进一步的解决。
