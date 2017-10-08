---
layout: post
title: "简单计算器代码"
date: 2015-3-4 20:14
description: "使用C语言实现简单的计算器代码"
tag: C
---


今天开始正式接触计算机了，以前总感觉代码好神奇，就几个英文加一些看不懂的符号就能做成一个在电脑和手机上能看见的东西，还有很多有趣的功能。这是我第一次学习C语言时模仿着开始写的一个简单的计算机程序，第一次看见自己的成果还有点小激动呢，虽然只是一个黑色的框框（当时不知道那叫啥，后来百度了下原来叫cmd），也算迈出了第一步。

---
#include<stdio.h>
#include<conio.h>
void main()
{
printf("欢迎使用，请输入要计算的两个数，可以计算加减乘除，输入的数字为整数\n");
int a,b;
char c;
scanf("%d%c%d",&a,&c,&b);
switch(c)
{
case '+':printf("%d%c%d=%d\n",a,c,b,a+b);break;
case '-':printf("%d%c%d=%d\n",a,c,b,a-b);break;
case '*':printf("%d%c%d=%d\n",a,c,b,a*b);break;
case '/':printf("%d%c%d=%d\n",a,c,b,a/b);break;
defaul:printf("输入错误\n");   
}
getch();
}
