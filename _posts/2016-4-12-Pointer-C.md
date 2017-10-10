---
layout: post
title: "通過指針比較兩個數的大小"
date: 2016-4-12 23:28
description: "通過指針比較兩個數的大小"
tag: C
---


指针，没听过，感觉好高端，听老师说很难，哇，这不是打击了我们么(╯‵□′)╯︵┻━┻，我不管我就要看

```
#include<stdio.h>
#include<stdlib.h>
int main()
{
 double a, b, max, *pa, *pb,*pmax;
 pa = &a;
 pb = &b;
 pmax = &max;
 printf("請輸入第一個要比較的數：\n");
 scanf_s("%lf",pa);
 printf("請輸入第二個要比較的數：\n");
 scanf_s("%lf", pb);
 *pmax = *pa;
 if (*pb >*pa)
  *pmax =* pb;
 printf("最大的數是：%lf\n",max);
 system("pause");
}
```
