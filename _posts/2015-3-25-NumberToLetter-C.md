---
layout: post
title: "将数字转换为字母 "
date: 2015-3-4 20:14
description: "将数字转换为字母 "
tag: C
---


今天学习了ascll表，不得不说那个表是真的多，头都看大了，但是为了自己还是得记啊，

<pre>
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

最后附上ascll表
<div align="center">
	<img src="/images/image/ascll.jpg" height="954" width="652" />
</div>
