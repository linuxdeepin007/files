---
title: EXCEL 合并表格填充编号
date: 2022-09-03
categories:
   - 编程电脑
   - 办公软件
   - EXCEL
tags: 
   - 合并单元格
   - EXCEL
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

![填充单元格编号](https://github.com/linuxdeepin007/files/blob/main/BLOG/%E5%90%88%E5%B9%B6%E5%8D%95%E5%85%83%E6%A0%BC%E5%A1%AB%E5%85%85%E7%BC%96%E5%8F%B7.gif)
