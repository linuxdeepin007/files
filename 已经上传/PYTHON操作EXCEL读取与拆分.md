---
title: PYTHON操作EXCEL读取与拆分
date: 2022-07-23
categories:
   - 编程电脑
   - PYTHON
tags: 
   - PYTHON
   - EXCEL
   - 办公自动化 
---

PYTHON办公自动化内容，通过使用插件`.xlsx / .xlsm / .xltx / .xltm，`操作EXCEL，读取excel的插件为`openpyxl`
<!-- more -->

## 一、读取sheet名称

```python
from openpyxl import load_workbook

workbookname = load_workbook(filename=r"C:\Users\pdsat\Desktop\test.xlsx")
i = workbookname.sheetnames
print(i)

结果：
['电视剧', '动漫', '综艺', '图书书籍漫画', '教育资源', '神站', '小初高教育', '电影', '盘搜1', '考研教育资源', '盘搜2', '游戏软件', '学而思精品内容']
```

## 二、向表格中插入行数据

使用`.append()`在数据后面增加行数据

```python
from openpyxl import load_workbook

workbook_name = load_workbook(filename=r"C:\Users\pdsat\Desktop\test.xlsx")
sheet = workbook_name.active
print(sheet)
data = [
    ["唐僧", "https://www.daohangpage.com/site/335.html"],
    ["导航页面", "https://9kan.online/"],
    ["hao123", "https://m.hao123.com"]
]
for row in data:
    sheet.append(row)
workbook_name.save(filename=r"C:\Users\pdsat\Desktop\test.xlsx")
```

## 三、合并拆分sheet

```python
importopenpyxl

myBook=openpyxl.load_workbook(r"c:\users\pdsat\Desktop\A305\录取表.xlsx")
mySheet=myBook["录取表"]# 获取sheet工作簿
myRange=list(mySheet.values)
# mySheet.values 返回的是生成器，是将一行数据作为一个元组单元组成的，是由值组成的.
# Python 的元组与列表类似，不同之处在于元组的元素不能修改。
# 元组使用小括号，列表使用方括号。
# mySheet.values 获取的内容是从 “A1” 到 “最大行最大列”
myDisc={}# 新建一个字典
# 字典是另一种可变容器模型，且可存储任意类型对象。
# 字典的每个键值 key:value 对用冒号 : 分割，每个键值对之间用逗号 , 分割，
# 整个字典包括在花括号 {} 中 .
formyRowinmyRange[3:]:
ifmyRow[0]inmyDisc.keys():
myDisc[myRow[0]] += [myRow]
else:
myDisc[myRow[0]] = [myRow]
formyKey, myValueinmyDisc.items():
myNewSheet=myBook.create_sheet(myKey+'录取表')
myNewSheet.append(myRange[2])# 在新表中新建表头
formyRowinmyValue:
myNewSheet.append(myRow)
myBook.save(r'C:\Users\pdsat\Desktop\A305\新录取表.xlsx')

```