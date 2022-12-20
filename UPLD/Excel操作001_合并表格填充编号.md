---
title: Excel操作001_合并表格填充编号
date: 2022-09-03
categories:
   - 编程电脑
   - 办公软件
   - Excel
tags: 
   - 合并单元格
   - Excel
   - 编号 
---

我们可以通过下拉填充单元格编号，但是对于有合并单元格的表格，无法通过下拉来填充编号，通过使用公式，可以完成操作。且删除任意单元格，标号顺序自动更新。
<!-- more -->

## 一、软件版本

office2010+、WPS

## 二、操作步骤

1. 选中需要填充序号的单元格；
2. 按住Ctrl，点击第一个单元格
3. 输入`=MAX($A$1:A1)+1`或者`=ROW()-1`
4. Ctrl+Enter

## 三、效果图

![填充单元格编号](https://preview.cloud.189.cn/image/imageAction?param=DCFCBC1578F4E5E425606D9554871780FF4C49290967B04653018C98BEE61BEF995312E0881E648EEF0D035B3493FF04F7ACF1750AF98C9C99AC82EA4F8AAF3D110212B5776D6EDFB318EAF95C8C960096CE6B0E8F55C4FA7F62EC4342B4E2BEEA5B73F821304FD4F410C9A1D15F4449)
