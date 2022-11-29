---
title: LINUX下增加交换分区（swap）大小
date: 2022-08-14 
categories:
  - 编程电脑
  - LINUX
tags: 
   - LINUX
   - swap
   - 分区	
---
swap分区，即交换区。当系统的物理内存不够用的时候，就需要将物理内存中的一部分空间释放出来，以供当前运行的程序使用。
<!-- more -->
但是linux在安装过程中，默认的swap分区一般都很小，所以需要手动分区或者在系统安装好之后，再调整其大小。

## 一、当前系统配置

- linux（ubuntu）

```bash
linux@linux:~$ cat /proc/version
Linux version 4.15.0-175-generic (buildd@lcy02-amd64-034) (gcc version 7.5.0 (Ubuntu 7.5.0-3ubuntu1~18.04)) #184-Ubuntu SMP Thu Mar 24 17:48:36 UTC 2022
  
```

  

- 当前系统配置

```bash
linux@linux:~$ free -mh
                总计         已用        空闲      共享    缓冲/缓存    可用
  内存：        1.8G        806M        132M        130M        900M        691M
  交换：        974M        6.8M        968M
  
```

  

## 二、交换分区（swap）

### （一）交换分区作用

swap分区，即交换区，swap空间的作用可简单描述为：当系统的物理内存不够用的时候，就需要将物理内存中的一部分空间释放出来，以供当前运行的程序使用。

那些被释放的空间可能来自一些很长时间没有什么操作的程序，这些被释放的空间被临时保存到Swap空间中，等到那些程序要运行时，再从Swap中恢复保存的数据到内存中。

### （二）交换分区大小

在linux中，我们对swap分区的划分有一定的规则，当物理内存小于2G时，swap分区大小为物理内存的2倍；超过2G的部分，swap分区大小跟物理内存相等。

## 三、增加交换分区

### （一）新建一个swap文件

```bash
linux@linux:~$ dd if=/dev/zero of=/tmp/swap2 bs=1M count=4000 # 新建一个4G的文件，命名为swap2
记录了4000+0 的读入
记录了4000+0 的写出
4194304000 bytes (4.2 GB, 3.9 GiB) copied, 48.3163 s, 86.8 MB/s

```

### （二）设置并启用swap分区

```bash
linux@linux:~$ mkswap /tmp/swap2 # 设置为swap
mkswap: /tmp/swap2：不安全的权限 0664，建议使用 0600。
正在设置交换空间版本 1，大小 = 3.9 GiB (4194299904  个字节)
无标签， UUID=b3213bf5-7d34-448b-b16d-2ad5f14b7608
linux@linux:~$ sudo swapon /tmp/swap2 # 启用swap
[sudo] linux 的密码： 
swapon: /tmp/swap2：不安全的权限 0664，建议使用 0600。
swapon: /tmp/swap2：不安全的文件拥有者 1000，建议使用 0(root)。
```

### （三）查看当前swap分区大小

```bash
inux@linux:~$ free -hm
              总计         已用        空闲      共享    缓冲/缓存    可用
内存：        1.8G        888M        147M        204M        803M        533M
交换：        4.9G        212M        4.7G
```

## 三、永久设置及取消设置

### （一）永久设置swap分区

在配置文件末尾增加`linux@linux:~$ sudo gedit /etc/fstab` 

```bash
linux@linux:~$ sudo gedit /etc/fstab # 打开配置文件
```

### （二）取消swap分区

- 关闭swap2文件并删除

```bash
swapoff /tmp/swap2
rm -rf /tmp/swap2
```

- 修改配置文件
<<<<<<< HEAD
=======

>>>>>>> 674a6daf68e3f3f257715aba490f2170e5a61265
将 /etc/fstab中添加的末行删除
