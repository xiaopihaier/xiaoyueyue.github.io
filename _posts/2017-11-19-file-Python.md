---
layout: post
title: "Python实现txt文本文档内容查重"
date: 2017-11-19 23:39
description: "Python实现txt文本文档内容查重"
tag: Python
---
有时候我们有一个庞大的txt文件内容，而且里面有许多重复的内容，我们不可能一个一个用肉眼看呗，ps：那样会出事的，而且效率也没有电脑来的快。so，今天我们就用Python来实现一个txt文本内容的查重，并且支持图形化的界面和文件位置的选择，那让我们开始吧。

一：
    要想查出txt文件中的重复项我们就得知道txt文本中的内容，现在我们先来实现读取文本的内容，并写入另一个文件中。这里因为我们要操作文本文件，所以我们要导入os这个库，具体代码如下（这里我们先将文件放在桌面，并将文件名改为重复文件）：
```
import os

file = getpass.getuser() + ""
listA = open("C:\\Users\\" + file + "\\Desktop\\重复文件.txt", 'r').readlines()  # 读文件
            setB = set()
            for x in listA:
                if listA.count(x) == 1:
                    setB.add(x)
            fB = open('C:\\唯一.txt', "w")
            fB.writelines(setB)  # 写文件
            fB.writelines("\n")  # 写文件
            fB.close()

            listA = open("C:\\Users\\" + file + "\\Desktop\\重复文件.txt", 'r').readlines()  # 读文件
            setB = set()
            for x in listA:
                if listA.count(x) > 1:
                    setB.add(x)
            fB = open('C:\列出重复.txt', "w")
            fB.writelines(setB)  # 写文件
            fB.writelines("\n")  # 写文件
            fB.close()

            listA = open('C:\\唯一.txt', 'r').readlines()  # 读文件
            setB = set()
            for x in listA:
                if listA.count(x) == 1:
                    setB.add(x)
            fB = open("C:\\Users\\" + file + "\\Desktop\\最后结果.txt", "w")
            fB.writelines(setB)  # 写文件
            fB.writelines("\n")  # 写文件
            fB.close()

            listA = open('C:\\列出重复.txt', 'r').readlines()  # 读文件
            setB = set()
            for x in listA:
                if listA.count(x) == 1:
                    setB.add(x)
            fB = open("C:\\Users\\" + file + "\\Desktop\\最后结果.txt", "a")
            fB.writelines(setB)  # 写文件
            fB.writelines("\n")  # 写文件
            fB.close()

            os.remove('C:\\唯一.txt')
            os.remove('C:\\列出重复.txt')
```
