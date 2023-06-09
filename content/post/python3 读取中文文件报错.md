---
title: "python3 读取中文文件报错"
date: 2019-07-22T16:06:07+08:00
description: "《python让繁琐的工作自动化》笔记"
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: inner
tocLevels: ["h2", "h3", "h4"]
tags:
- "python"
categories:
- "编程语言"
series:
- "技术研究"
image: 
---

尝试读取car.txt，内容是中文，结果报错了

```python
Traceback (most recent call last):
  File "fix.py", line 12, in <module>
    for each_line in car.readlines():
UnicodeDecodeError: 'gbk' codec can't decode byte 0xa1 in position 4: illegal mu
ltibyte sequence
```

## 问题代码

```python
cars = open(r".\car.txt")
for each_line in cars.readlines():
	print(each_line)
print("完成！")

cars.close()
```

## 解决方法

- open函数可选参数
```python
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)
```
- 根据报错，中文编码是“gbk”
- 所以，要把encoding参数设置为“utf-8”,才能正确处理中文文本。
- 以防万一，errors参数，设置为“ignore”， 忽略报错&警告（一般不用）

```python
car = open(r".\car.txt", encoding='utf-8', errors='ignore')
```
ok，可以正确处理有中文的文件了。

```python
skip
... ...
南京依维柯宝迪
奇瑞风云 旗云1.3 马自达2 1.3
奇瑞旗云1.6
奇瑞A3 瑞虎
完成！
```