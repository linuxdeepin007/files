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

![填充单元格编号](https://preview.cloud.189.cn/image/imageAction?param=F52E0658E77DF2FC08199FDDF4DB3E1495EFC3B1E8421C2D0F5717D4FAAFB621D8BB05A91606CBC30A1947A2EC0635D4F5D4878A521E09191B60545025D3854CB0E9F99E4C7502FD0F5743EBC926C7B93D4BC75A5EC8E6FCEA59B8F10BCEA5B289877518DD56628E2E1288136D62F008)
