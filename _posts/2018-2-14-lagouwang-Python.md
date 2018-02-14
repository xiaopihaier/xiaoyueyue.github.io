---
layout: post
title: "爬取拉勾网招聘信息"
date: 2018-2-14 10:51
description: "使用python爬取拉勾网招聘信息"
tag: python
---

今天带大家实现通过python实现拉钩网招聘信息的爬取，准备工具如下:([python2.7.14](https://www.python.org/downloads/)、[pycharm](http://www.jetbrains.com/pycharm/download/#section=windows))。开始代码前的准备工作：安装python、pycharm，安装完工具后打开cmd工具输入分别输入：pip install bs4、pip install requests安装bs4和requests包。一切准备就绪后开始我们的代码编写,打开拉勾网网址登陆并输入如python，并复制地址栏的网址以备使用。

```
# coding 'utf-8'

import requests


def main():
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) '
                      'Chrome/64.0.3282.167 '
                      'Safari/537.36 ',
        'Host': 'www.lagou.com'
    }
    result = requests.get("https://www.lagou.com/jobs/list_python?city=%E6%88%90%E9%83%BD&cl=false&fromSearch=true"
                          "&labelWords=&suginput=", headers=headers)
    print result.content


if __name__ == '__main__':
    main()

```
