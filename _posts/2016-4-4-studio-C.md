---
layout: post
title: "学生成绩管理系统"
date: 2016-4-4 20:14
description: "学生成绩管理系统"
tag: C
---


今天来做一个高端的东西，学生成绩管理系统，o(*￣▽￣*)ブ，听起来就很高大上吧，我也是这样认为的，让我们一起来看看吧

```
#include<stdio.h>
#include<stdlib.h>
int main()
{
	struct student
	{
		long no; /*学号*/
		char name[10]; /*姓名*/
		char sex; /*性别*/
		int age; /*年龄*/
		float score; /*平均成绩*/
	};
	struct student stu[6];
	int n, i,j,d = 0, c = 0;
	int M = 0, W = 0;
	printf("请输入人数：");
	scanf("%d", &n);
	printf("学号 姓名 性别（男：M 女：W）  年龄 成绩\n");
	for (i = 0; i < n; i++)
	{
		scanf("%d %s %c %d %f", &stu[i].no, stu[i].name, &stu[i].sex, &stu[i].age, &stu[i].score);
	}
	for (j = 0; j <= n - 1; j++)
	{
		d = d + stu[j].score;
	}
	c = d / n;
	printf("\n\n");
	for (i = 0; i < n; i++)
		printf("%d %s %c %d %f\n", stu[i].no, stu[i].name, stu[i].sex, stu[i].age, stu[i].score);
	printf("平均分：%d\n", c);
	printf("低于平均分的是：\n");
	for (i = 0; i < n; i++)
	{
		if (stu[i].score < c)
			printf("%d %s %c %d %f\n", stu[i].no, stu[i].name, stu[i].sex, stu[i].age, stu[i].score);
	}
	for (i = 0; i < n; i++)
	{
		if (stu[i].sex =='M')
			M++;
		if (stu[i].sex == 'W')
			W++;
	}
	printf("男：%d\n女：%d\n",M,W);
	system("pause");
}
```
