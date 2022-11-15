---
title: 使用Grub Rescue 修复linux启动失败
date: 2022-07-07
categories:
   - 编程电脑
   - LINUX
tags: 
   - GRUB
   - boot failure
   - 双系统 
---
 GRUB (Grand Unified Bootloader)，是引导系统的工具，当安装双系统（linux+windows）时，win启动会覆盖grub，导致无法启动系统。本文介绍了两种方法修复启动失败的问题。
<!-- more -->
# 一、系统启动失败

## （一）系统启动失败情况

linux系统启动失败出现grub rescue的情况是由于多系统启动，启动文件丢失或者被覆盖导致的。当启动失败时，通常会出现如下界面：

```bash
error : no such partition.
Entering rescue mode...
grub rescue> _
```

或者是：

```bash
error : unknown filesystem.
Entering rescue mode...
grub rescue> _
```

亦或者：

```bash
grub rescue> _
```

## （二）相关命令

|命令|解释|示例 / 选项|
|:----|:----|:----|
|boot|启动|直接启动系统|
|cat|标准输出|cat (hd0,1)/boot/grub/grub.cfg|
|configfile|载入配置文件|configfile (hd0,1)/boot/grub/grub.cfg|
|initrd|载入initrd.img 文件|initrd (hd0,1)/initrd.img|
|insmod|载入模式|insmod (hd0,1)/boot/grub/normal.mod|
|loopback|挂在镜像为设备|loopback loop0 (hd0,1)/iso/image.iso|
|ls|列举文件及目录|	ls (hd0,1)|
|lsmod|列举所有模式|-|
|normal|激活普通模式|+|
|search|查找设备：--file 查找文件； --label 查找标签, --fs-uuid 查找系统文件 UUID.|search -file [filename]|
|set|设置环境变量如果没有选项，则输出所有环境变量和值。|set [variable-name]=[value]|

# 二、修复方法
教程中提供两种修复grub的方法命令行操作和启动盘操作

## （一）通过命令行修复
### 1. 使用`set`命令，查看环境变量
如下，该系统启动自`（hd0,msdos3）`

```bash
grub> set
?=0
color_highlight=black/white
color_normal=white/black
default=0
gfxmode=800x600
lang=en_US
locale_dir=(hd0,msdos3)/boot/grub/local
pager=
prefix=(hd0,msdos3)/boot/grub
root=hd0,msdos3
grub> _
```

### 2. 使用`ls`命令，查看分区表

```bash
grub> ls
(hd0) (hd0,msdos3) (hd0,msdos2) (hd0,msdos1)
grub> _
```

### 3. 查找包含`boot`目录的分区

```bash
grub> ls （hd0,msdos3）
lost+found var/ dev/ run/ etc/ tmp/ sys/ proc/ usr/ bin boot/ lib lib64 mnt/ opt/ root/ sbin srv/
grub> _
```

### 4. 设置启动分区作为`root`变量所在卷

```bash
set root=(hd0,msdos1)
```

### 5. 载入`normal`启动模式

```bash
insmod normal
```

### 6. 启动normal 启动模式

```bash
normal
```

### 7. 使用`linux`载入linux内核

```bash
linux /boot/vmlinuz-4.2.0-16-generic root=/dev/sda1 ro
```

### 8. 启动

```bash
boot
```

## （二）通过启动盘修复

### 1. 制作linux启动安装盘并启动试用模式

### 2. 打开终端输入命令

```bash
sudo add-apt-repository ppa:yannubuntu/boot-repair
```
### 3. 在终端中安装并启动软件

```bash
sudo apt update
sudo apt install boot-repair
boot-repair
```
### 4. 等待修复完成重启电脑

# 三、更新GRUB 启动文件
在系统重新启动之后，要重新配置grub，以确保安装成功

```bash
sudo update-grub
```