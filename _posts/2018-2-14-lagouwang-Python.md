---
layout: post
title: "爬取拉勾网招聘信息"
date: 2018-2-14 10:51
description: "使用python爬取拉勾网招聘信息"
tag: python
---

今天带大家实现通过python实现拉钩网招聘信息的爬取，准备工具如下：python2.7.14（下载地址：[example link]https://www.python.org
/downloads/）、
pycharm（下载地址：http://www.jetbrains.com/pycharm/download/#section=windows）。开始代码前的准备工作：安装python、pycharm，安装完工具后打开cmd工具输入分别输入：pip install bs4、pip install requests安装bs4和requests包。一切准备就绪后开始我们的代码编写,打开拉勾网网址登陆并输入如‘C’字符，并复制地址栏的网址以备使用。

```
# coding 'utf-8'

import requests
from bs4 import BeautifulSoup


def main():
    result = requests.get("https://www.lagou.com/jobs/list_c?labelWords=&fromSearch=true&suginput=")
    print result.content


if __name__ == '__main__':
    main()

```
