---
title: 在linux系统上搭建个人博客（hexo+gitee）
date: 2022-04-10 
categories:
  - 电脑编程
  - HEXO
tags: 
   - HEXO
   - BUG
   - 网页	
---
到今天为止，个人博客算是搭建完成了。从看教程到上手操作，前前后后折腾了一天多的时间。主要的问题集中在两个方面：一是如何让网页在本地运行；另外就是如何让网页在gitee page上运行。
<!-- more -->

## 一、linux系统
在搭建个人博客之前，选择一个熟悉的系统还是相当重要的，由于linux天生优势，加之目前使用的电脑过于老旧，所以我选择了在linux系统下搭建个人博客。需要部署包括`Nodejs` `git`等在内的环境，这里强烈建议备份系统，如果系统内各种软件无法“和平相处”的时候，可以一键还原。

### 1.1 备份linux系统
在备份系统之前，准备一个linux系统安装盘，便于在图形界面下操作。我使用的是xbuntu系统，其他linux发行版本大同小异。

#### 使用tar命令备份
和windows系统不同，linux中root用户可以为所欲为，甚至可以将系统本身删除，参考删库跑路操作，所以首先切换到root用户，进行如下操作：
```bash
linux@linux:~/hexo/blog/blogs$ su root
密码： 
root@linux:/home/linux/hexo/blog/blogs# cd /
root@linux:/# tar cvpzf backup.tgz --exclude=/proc --exclude=/lost+found --exclude=/backup.tgz --exclude=/mnt --exclude=/sys /

```
tar 命令解释：
- “tar”当然就是我们备份系统所使用的程序了。
- “cvpfz”是tar的选项，意思是“创建档案文件”、“保持权限”(保留所有东西原来的权限)、“使用gzip来减小文件尺寸”。
- “backup.gz”是我们将要得到的档案文件的文件名。
- “/”是我们要备份的目录，在这里是整个文件系统。
- 在 档案文件名“backup.gz”和要备份的目录名“/”之间给出了备份时必须排除在外的目录。

> 有些目录是无用的，例如“/proc”、“/lost+ found”、“/sys”。当然，“backup.gz”这个档案文件本身必须排除在外，否>则你可能会得到一些超出常理的结果。如果不把“/mnt”排 除在外，那么挂载在“/mnt”上的其它分区也会被备份。另外需要确认一下“/media”上没有挂载任何东西(例如光盘、移动硬盘)，如果有挂载东西， 必须把“/media”也排除在外。

备份完成后，在文件系统的根目录将生成一个名为“backup.tgz”的文件，它的尺寸有可能非常大。现在你可以把它烧录到DVD上或者放到你认为安全的地方去。在备份命令结束时你可能会看到这样一个提示：’tar: Error exit delayed from previous errors’，多数情况下你可以忽略它。

你还可以用Bzip2来压缩文件，Bzip2比gzip的压缩率高，但是速度慢一些。如果压缩率对你来说很重要，那么你应该使用Bzip2，用“j”代替命令中的“z”，并且给档案文件一个正确的扩展名“bz2”。完整的命令如下： 
```bash
# tar cvpjf backup.tar.bz2  --exclude=/proc  --exclude=/lost+found  --exclude=/backup.tar.bz2  --exclude=/mnt  --exclude=/sys /
```
### 1.2 恢复linux系统

#### 使用tar命令恢复系统
在进行恢复系统的操作时一定要小心！如果你不清楚自己在做什么，那么你有可能把重要的数据弄丢，请务必小心！

在 Linux中有一件很美妙的事情，就是你可以在一个运行的系统中恢复系统，而不需要用boot-cd来专门引导。当然，如果你的系统已经挂掉不能启动了，你可以用Live CD来启动，效果是一样的。你还可以用一个命令把Linux系统中的所有文件干掉。
使用下面的命令来恢复：

```bash
# tar xvpfz backup.tgz -C /
```
如果你的档案文件是使用Bzip2压缩的，应该用： 
```bash
# tar xvpfj backup.tar.bz2 -C /
```

### 1.3注意事项
该命令是在可以启动的系统上恢复，为了能够更加彻底干净地恢复系统，建议使用live-CD，进入后删除文件系统内所有内容，然后恢复，此时恢复目录就不是‘/’，而是带有一串数字，挂载在/media下面的一个目录，否则将恢复到live-CD目录，导致系统乱码卡死。

## 二、使用hexo搭建个人博客
此时，你就可以随心所欲地搭建个人博客，不用担心系统会不会被自己折腾坏了，大不了直接恢复系统，由于文件本身就在系统盘上，使用`tar`命令压缩，操作速度很快。

### 2.1 注册github或者gitee（码云）账号

推荐码云账号，网速快：注册点击[这里](https://gitee.com/);
注：新建仓库时，用户名和仓库名需保持一致,原因是生成的默认pages地址好看。


### 2.2 安装Hexo
在个人文件夹下新建本地博客文件夹，我的是hexo/blog

```bash
linux@linux:~/hexo/blog/blogs$ npm install -g hexo
```
耐心等一会儿，可能会失败，多试几次就可以了，网上的帖子有提到用淘宝的cnpm安装，个人不建议，后期可能会出现莫名其妙的错误。下载完成后，你会得到这样一个结构的文件夹

```bash
.
├── _config.fluid.yml
├── _config.landscape.yml
├── _config.yml
├── db.json
├── node_modules
├── package.json
├── package-lock.json
├── public
├── scaffolds
├── source
└── themes

```

### 2.3 安装主题（fluid）
方式一：

```bash
npm install --save hexo-theme-fluid
```

然后在博客目录下创建 _config.fluid.yml，将主题的 _config.yml 内容复制进去。

方式二：

```bash
git clone https://github.com/fluid-dev/hexo-theme-fluid.git
```

直接下载压缩文件，解压后放到themes目录，将解压出来的文件夹命名为fluid

### 2.4修改配置

#### 修改配置
修改 Hexo 博客目录中的 _config.yml：
```bash
theme: fluid  # 指定主题
language: zh-CN  # 指定语言，会影响主题显示的语言，按需修改
```

#### 创建主页
首次使用主题的「关于页」需要手动创建：

```bash
hexo new page about
```

创建成功后，编辑博客目录下 /source/about/index.md，添加 layout 属性。
修改后的文件示例如下：

```bash
---
title: about
date: 2020-02-23 19:20:33
layout: about
---

这里写关于页的正文，支持 Markdown, HTML
```

具体详细的配置美化参考文章：[hexo美化](https://blog.csdn.net/weixin_49270402/article/details/117672195).

## 三、部署到gitee page上

### 3.1 修改配置
打开_config.yml文件，到Deployment下进行修改：更换url处的网址。
执行命令

```bash
$ npm install hexo-deployer-git --save

```

### 3.2 部署静态服务
点击服务--> Gitee Pages。
此处直接生成，注意勾选强制http，否则生成的页面显示不全。

### 3.3 生成本地密钥

```bash
git config --global user.name "yourname"
git config --global user.email "youremail"
ssh-keygen -t rsa -C "youremail"
```

默认生成秘钥key在\.ssh文件夹下。在个人设置里，点击SSH公钥，添加公钥，标题自己随便选，公钥就是本地生成的id_rsa.pub里面的内容。

### 3.4 更新代码

```bash
$ hexo clean //每次修改完 _config.yml 后都要执行一边这个命令行
$ hexo g  //部署之前预先生成静态文件
$ hexo d  //部署网站
```

每次提交更新后的代码，都要重新运行以上代码，同时重新生成gitee page页面。
