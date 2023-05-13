---
title: Vim 常用操作
date: 2023-05-13 20:52:12
tags:
    - linux
categories: linux
cover: http://cdn.frankfurtlin.top/blog/covers/cover12.jpg
---

# Vim 常用操作

## 全选文件

``` vim
# gg 跳转到文件首行
# V 进入可视模式，选中行
# G 跳到文件尾行
ggVG
```

## 字符串替换

``` vim
在 Vim 中，要实现字符串替换，可以使用 substitute 命令 :substitute，简写为 :s。
语法为:
:[range]s/pattern/string/flags
- [range] 表示要替换的行范围,可选
- pattern 表示要查找的模式
- string 表示替换的字符串
- flags 表示替换标记,可选,包括:
  - g 全局替换
  - c 确认替换
  - i 忽略大小写
  
例如:
1. 将当前行的第一个 hello 替换为 hi:
:s/hello/hi

2. 将第3到5行所有的 hello 替换为 hi:
:3,5s/hello/hi/g

3. 交互模式替换第3行的hello:
:3s/hello//c   
然后Vim会提示:
replace with:
用户输入hi并回车,完成替换。

4. 忽略大小写替换全文hello为hi:
:1,$s/hello/hi/gi
1,$ 代表全文行范围。
```