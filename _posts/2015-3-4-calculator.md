---
layout: post
title: "简单计算器代码"
date: 2015-3-4 20:14
description: "使用C语言实现简单的计算器代码"
tag: iOS
---


```
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
}```
