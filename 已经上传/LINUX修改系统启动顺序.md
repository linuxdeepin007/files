---
title: LINUX修改系统启动顺序
date: 2022-06-23
categories:
   - 编程电脑
   - LINUX
tags: 
   - 启动顺序
   - 系统
   - LINUX 
---

多系统引导，修改grub启动顺序。
<!-- more -->

# 修改grub文件
直接修改grub文件，位置/etc/defauts/grub

```bash
linux@linux-Vostro-260:~$ sudo gedit /etc/default/grub
[sudo] password for linux:

______________________________________________________________
# If you change this file, run 'update-grub' afterwards to update
# /boot/grub/grub.cfg.
# For full documentation of the options in this file, see:
#   info -f grub -n 'Simple configuration'

GRUB_DEFAULT=4
GRUB_TIMEOUT_STYLE=hidden
GRUB_TIMEOUT=8
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
GRUB_CMDLINE_LINUX=""

# Uncomment to enable BadRAM filtering, modify to suit your needs
# This works with Linux (no patch required) and with any kernel that obtains
# the memory map information from GRUB (GNU Mach, kernel of FreeBSD ...)
#GRUB_BADRAM="0x01234567,0xfefefefe,0x89abcdef,0xefefefef"
```
GRUB_DEFAULT=4，其中第一项是0，第二项是1,以此类推。以本机的启动选项来说，如果将最后一个作为启动默认选项，则数字为4