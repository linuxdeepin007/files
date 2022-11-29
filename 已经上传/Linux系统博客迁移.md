---
title: LINUX系统电脑上迁移博客系统
date: 2022-11-01
categories:
   - 编程电脑
   - LINUX
tags: 
   - 博客
   - 迁移
   - 环境 
---

适用于重新安装系统或者迁移到另外一台电脑，需要重新配置环境。搭建环境：linux-ubuntu，20.04.01,。win环境下还未尝试。
<!-- more -->

## 一、linux系统上迁移

### （一）备份文件复制到文件夹
需要实时更新备份文件

### （二）安装升级必要的软件
软件包括：npm\git\nodejs

```bash
linux@linux-ThinkCentre-E75:~/文档/blogs$ sudo apt install npm # 有时候因为版本不对报错，需要把nodejs升级到最新版本
```

1. 产看node版本，没安装的请先安装；

```
 linux@linux-ThinkCentre-E75:~/文档/blogs$ node -v
```

2. 如果安装失败，清除node缓存；

```
linux@linux-ThinkCentre-E75:~/文档/blogs$ sudo npm cache clean -f  
```

3. 安装node版本管理工具'n';

```
linux@linux-ThinkCentre-E75:~/文档/blogs$ sudo npm install n -g
```

4. 使用版本管理工具安装指定node或者升级到最新node版本；

```
linux@linux-ThinkCentre-E75:~/文档/blogs$ sudo n stable  （安装node最新版本）
```

5. 安装hexo

```bash
linux@linux-ThinkCentre-E75:~/文档/blogs$ sudo npm install -g hexo

```

### （三）通过ssh keys绑定gitee/github

1. 生成密钥（回车三次）

```bash
linux@linux-ThinkCentre-E75:~/文档/blogs$ ssh-keygen -t ed25519 -C "bs0716@126.com"  
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/linux/.ssh/id_ed25519): 
Created directory '/home/linux/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/linux/.ssh/id_ed25519
Your public key has been saved in /home/linux/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:w1pBqIn8XtBaNIQIEo/pTOjqJxssGiQH7REkRB4zNyA bs0716@126.com
The key's randomart image is:
+--[ED25519 256]--+
|E@++ o...        |
|=**.o +.         |
|=++. = ..        |
|=oo.+ o. .       |
|.=o. +  S        |
|=.  o .o .       |
|+o . ..          |
|+o...            |
|.o+              |
+----[SHA256]-----+
linux@linux-ThinkCentre-E75:~/文档/blogs$
```
在github中的命令

```bash
linux@linux-Lenovo-XiaoXinPro-13API-2019:~$ ssh-keygen -t rsa -C 'linuxdeepin007@gmail.com'
Generating public/private rsa key pair.
Enter file in which to save the key (/home/linux/.ssh/id_rsa): 
Created directory '/home/linux/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/linux/.ssh/id_rsa
Your public key has been saved in /home/linux/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:raNP4f208L04TjXseVXc6pIXWUA4HJicIFhGyDQizK8 linuxdeepin007@gmail.com
The key's randomart image is:
+---[RSA 3072]----+
|+ .oo== .o =.+o  |
| + .+o .  = +  o.|
|  .          .  =|
|   .     .   . +.|
|  .     S .   B .|
| E     . +   = +.|
|        = o = = .|
|       o . *.* . |
|      ...  .*.o. |
+----[SHA256]-----+
linux@linux-Lenovo-XiaoXinPro-13API-2019:~$ 

```

2. 通过查看 `~/.ssh/id_ed25519.pub` 公钥，和`~/.ssh/id_ed25519`获取对私钥文件内容，获取到你的 public key

```bash
linux@linux-ThinkCentre-E75:~/文档/blogs$ cat ~/.ssh/id_ed25519.pub
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIK/QJbu+k40c8i7ZioAdLRVwgOeNsO+Ea7aad1LdG9z7 bs0716@126.com

linux@linux-ThinkCentre-E75:~/文档/blogs$ cat ~/.ssh/id_ed25519
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACCv0CW7vpONHPIu2YqAHS0VcIDnjbDvhGu2mndS3Rvc+wAAAJiJxTPFicUz
xQAAAAtzc2gtZWQyNTUxOQAAACCv0CW7vpONHPIu2YqAHS0VcIDnjbDvhGu2mndS3Rvc+w
AAAECrAEvFII+Wco2D/c3kSQaAymNCLIo5FvlbG3axBB3H7q/QJbu+k40c8i7ZioAdLRVw
gOeNsO+Ea7aad1LdG9z7AAAADmJzMDcxNkAxMjYuY29tAQIDBAUGBw==
-----END OPENSSH PRIVATE KEY-----
linux@linux-ThinkCentre-E75:~/文档/blogs$
```

3.  首次确认，需要确认并添加主机到本机SSH可信列表
要注意按照命令提示输入 `yes`

```bash
linux@linux-ThinkCentre-E75:~/文档/blogs$ ssh -T git@gitee.com
The authenticity of host 'gitee.com (212.64.63.190)' can't be established.
ECDSA key fingerprint is SHA256:FQGC9Kn/eye1W8icdBgrQp+KkGYoFgbVr17bmjey0Wc.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'gitee.com,212.64.63.190' (ECDSA) to the list of known hosts.
Hi 望月砂! You've successfully authenticated, but GITEE.COM does not provide shell access.
linux@linux-ThinkCentre-E75:~/文档/blogs$
```

### （四）配置部署用户信息
按照官方文档确认身份标识。

```bash
```bash
linux@linux-ThinkCentre-E75:~/文档/blogs$ git config --global user.email "bs0716@126.com"
linux@linux-ThinkCentre-E75:~/文档/blogs$ git config --global user.name "linuxdeepin007"
<<<<<<< HEAD
=======
linux@linux-ThinkCentre-E75:~/文档/blogs$ hexo clean
>>>>>>> 674a6daf68e3f3f257715aba490f2170e5a61265
```
