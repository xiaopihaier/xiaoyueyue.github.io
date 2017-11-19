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
二：
  现在我们来实现图形化界面，实现更人性化的操作，我们导入tkinter库来实现图形界面的创建，具体代码如下：
  ```
from tkinter import Tk, Button, Text, filedialog, END


class Applicaton(object):
    def __init__(self):
        self.window = Tk()
        self.window.title('txt文件内容去重软件')
        self.window.geometry('250x200+400+200')

        self.text = Text(self.window, background='#ccc')
        self.text.place(x=10, y=10, width=200, height=20)

        self.button_openfile = Button(self.window, text=u'...', command=self.open_file)
        self.button_openfile.place(x=215, y=10, width=30, height=20)

        self.button_inspect = Button(self.window, text=u'开始检查', command=self.submit)
        self.button_inspect.place(x=98, y=35, width=60, height=20)

    def open_file(self):
        self.r = filedialog.askopenfilename(title='打开文件', filetypes=[('','txt')])
        content = os.path.basename(self.r)
        self.text.delete(1.0, END)
        self.text.insert(END, content)
        print(content)

    def submit(self):
        print(content)

    def run(self):
        self.window.mainloop()


if __name__ == '__main__':
    app = Applicaton()
    app.run()
  ```
这样我们就创建了一个图形化的界面，并且可以用户自己选择要打开的文件，现在我们通过把上面两个代码结合来创建一个完整的程序：
```
from tkinter import Tk, Button, Text, filedialog, END
import os
import getpass


class Applicaton(object):
    def __init__(self):
        self.window = Tk()
        self.window.title('txt文件内容去重软件')
        self.window.geometry('250x200+400+200')

        self.text = Text(self.window, background='#ccc')
        self.text.place(x=10, y=10, width=200, height=20)

        self.button_openfile = Button(self.window, text=u'...', command=self.open_file)
        self.button_openfile.place(x=215, y=10, width=30, height=20)

        self.button_inspect = Button(self.window, text=u'开始检查', command=self.submit)
        self.button_inspect.place(x=98, y=35, width=60, height=20)

        self.i = 0

    def open_file(self):
        self.r = filedialog.askopenfilename(title='打开文件', filetypes=[('','txt')])
        content = os.path.basename(self.r)
        self.text.delete(1.0, END)
        self.text.insert(END, content)
        print(content)
        self.i = 1

    def submit(self):
        if self.i == 1:
            print(self.r)
            file = getpass.getuser() + ""
            self.i = 0
            listA = open(self.r, 'r').readlines()  # 读文件
            setB = set()
            for x in listA:
                if listA.count(x) == 1:
                    setB.add(x)
            fB = open('C:\\唯一.txt', "w")
            fB.writelines(setB)  # 写文件
            fB.writelines("\n")  # 写文件
            fB.close()

            listA = open(self.r, 'r').readlines()  # 读文件
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

        else:
            print('请选择文件')

    def run(self):
        self.window.mainloop()


if __name__ == '__main__':
    app = Applicaton()
    app.run()
```

到此，教程结束，我们就写好了一个带界面的文件查重的程序啦，是不是满满的成就感啊，快快使用起来吧。
