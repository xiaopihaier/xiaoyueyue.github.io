---
layout: post
title: "利用结构体调用系统时间"
date: 2016-8-4 20:14
description: "利用结构体调用系统时间"
tag: C
---

显得无聊就做了一个显示系统时间的，做的还有点头大，差点就放弃了
<pre>
#include<stdio.h>
#include<stdlib.h>
#include<windows.h>
#include<time.h>
int main()
{
	time_t rawtime;
	struct tm*timeinfo;
	while (1)
	{
		time (&rawtime);
		timeinfo = localtime(&rawtime);
		printf("当前系统时间为：%s",asctime(timeinfo));
		Sleep(1000);
		system("cls");
	}
	system("pause");
}
