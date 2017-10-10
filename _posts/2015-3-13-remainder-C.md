---
layout: post
title: "输入两个数1500和350求出两数的商和余数并输出"
date: 2015-3-14 00:00
description: "输入两个数1500和350求出两数的商和余数并输出"
tag: C
---


今天来温习一下才学一段时间的除和取余的区别，除的话就只取除数，取余就只取余数。


```
#include<stdio.h>
#include<conio.h>
void main()
{
 int a=1500,b=350, s, y;
 s=a/b;
 y=a%b;
 printf("a和b的商为%d,a和b的余数为%d", s, y);
 getchar();
}
```
