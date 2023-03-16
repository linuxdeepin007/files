---
title: Python入门001_列表简介
date: 2022-08-17
categories:
   - 编程电脑
   - Python 
   - 入门课程
tags: 
   - Python
   - 列表
   - 数据类型 
---
列表 由一系列按特定顺序排列的元素组成。
<!-- more -->
你可以创建包含字母表中所有字母、数字0-9或所有家庭成员姓名的列表；也可以将任何东西加入列表中，其中的元素之间可以没有任何关系。列表通常包含多个元素。

## 一、列表的表示方法

在Python中，用方括号`[]`表示列表，并用逗号分隔其中的元素。 例如：

```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
```

运行结果

```python
['fenghuang', 'meili', 'taiyang', 'FBI']
```

## 二、列表的访问

### （一）列表是有序集合

因此要访问列表的任意元素，只需将该元素的位置（索引 ）指出列表的名称，再指出元素的索引，并将后者放在方括号内。
下面的代码从列表bicycles 中提取第一款自行车：

```python
print(bicycles[0])
```

运行结果

```python
fenghuang
```

### （二）访问最后一个元素

Python为访问最后一个列表元素提供了一种特殊语法。通过将索引指定为-1 ，可让Python返回最后一个列表元素

```python
print(bicycles[-1])

```

运行结果

```python
FBI
```

### （三）使用各个元素

你可以像使用其他变量一样使用列表中的各个值。

#### 格式化输入
>
> 从 Python 3.0 开始，format()函数被引入以提供高级格式化选项。

从 Python 3.6 开始，Python f 字符串可用。 该字符串具有f前缀，并使用{}评估变量。

```python
bags = 3
apples_in_bag = 12
print(f'There are total of {bags * apples_in_bag} apples')

```

运行结果

```python
There are total of 36 apples
```

## 三、列表的修改

创建的大多数列表将是动态的，将随着程序的运行增删元素。

### （一）修改列表元素

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)
motorcycles[0] = 'ducati'
print(motorcycles)
```

运行结果

```python
['honda', 'yamaha', 'suzuki']
['ducati', 'yamaha', 'suzuki']
```

### （二）在列表中添加元素

#### 1.在列表末尾添加元素

使用`append()` 办法，将元素附加 （append）到列表。

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)
motorcycles.append('ducati')
print(motorcycles)
```

运行结果

```python
['honda', 'yamaha', 'suzuki']
['honda', 'yamaha', 'suzuki', 'ducati']
```

#### 2.在列表中插入元素

使用方法`insert()`可在列表的任何位置添加新元素。

方法insert() 在索引0 处添加空间，并将值'ducati' 存储到这个地方。这种操作将列表中既有的每个元素都右移一个位置

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)
motorcycles.insert(0,'ducati')
print(motorcycles)
```

运行结果

```python
['honda', 'yamaha', 'suzuki']
['ducati', 'honda', 'yamaha', 'suzuki']
```

### （三）从列表中删除元素

#### 1.使用 `del` 语句删除元素

如果知道要删除的元素在列表中的位置，可使用 `del` 语句。

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)
del motorcycles[0]
print(motorcycles)
```

运行结果

```python
['honda', 'yamaha', 'suzuki']
['yamaha', 'suzuki']
```

#### 2.使用方法 `pop()` 删除元素

> 每当你使用pop() 时，被弹出的元素就不再在列表中了

方法pop() 删除列表末尾的元素，并让你能够接着使用它。列表就像一个栈，而删除列表末尾的元素相当于弹出栈顶元素。

案例需求：有时候，你要将元素从列表中删除，并接着使用它的值。例如，你可能需要获取刚被射杀的外星人的 坐标和 坐标，以便在相应的位置显示爆炸效果；在Web应用程序中，你可能要将用户从活跃成员列表中删除，并将其加入到非活跃成员列表中。

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

poped_motorcycles = motorcycles.pop()
print(motorcycles)
print(f'The last bicycle I owned was "{poped_motorcycles.title()}".')
```

运行结果

```python
['honda', 'yamaha', 'suzuki']
['honda', 'yamaha']
The last bicycle I owned was "Suzuki".
```

#### 3.根据值删除元素 `remove()`

有时候，你不知道要从列表中删除的值所处的位置,只知道要删除的元素的值，可使用方法`remove()`。

> 使用remove() 从列表中删除元素时，也可接着使用它的值。

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

removed_motorcycles = 'honda'
motorcycles.remove(removed_motorcycles)

print(motorcycles)
print(f'\nThe {removed_motorcycles.title()} is too expensive.')
```

<font face='楷体' color= blue> 运行结果：</font>

```PYTHON
['honda', 'yamaha', 'suzuki']
['yamaha', 'suzuki']

The Honda is too expensive.
```

## 四、组织列表

元素的排列顺序常常是无法预测的，有时候又需要调整排列顺序。

### （一）使用方法 `sort()` 对列表永久排序

列表会按照字母表顺序排序。与字母顺序相反的顺序排列列表元素，只需向sort() 方法传递参数reverse=True 即可

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(cars)
cars.sort()
print(cars)
cars.sort(reverse=True)
print(cars)
```

运行结果

```python
['bmw', 'audi', 'toyota', 'subaru']
['audi', 'bmw', 'subaru', 'toyota']
['toyota', 'subaru', 'bmw', 'audi']
```

### （二）使用函数 `sorted()` 对列表临时排序

函数sorted() 能够按特定顺序显示列表元素，同时不影响它们在列表中的原始排列顺序。

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(f'This is the original list:\n{cars}')
print('----------------------------')
print(f'This is the sorted list temporary list:\n{sorted(cars)}')
print('----------------------------')
print(f'This is the original list:\n{cars}')
```

输出结果

```python
This is the original list:
['bmw', 'audi', 'toyota', 'subaru']
----------------------------
This is the sorted list temporary list:
['audi', 'bmw', 'subaru', 'toyota']
----------------------------
This is the original list:
['bmw', 'audi', 'toyota', 'subaru']
```

### （三）确定列表的长度 `len()`

使用函数 `len()` 可快速获悉列表的长度。

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(len(cars))
```

输出结果

```
4
```
