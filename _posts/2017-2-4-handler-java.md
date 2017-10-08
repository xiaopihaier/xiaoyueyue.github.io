---
layout: post
title: "多线程实现存取金钱"
date: 2016-2-4 20:14
description: "多线程实现存取金钱"
tag: java
---

多线程大家应该都不陌生吧，你边听歌边玩儿游戏，CPU同时要处理两个东西吧，其实并不是同时处理的，这就是多个线程交替的来进行的，只是时间非常的短，就让大家认为是同时处理的，今天就通过多线程来实现java存取钱的显示
<pre>
package com.xiaopihaier.多线程;

import java.util.Scanner;

public class 多线程 {
static int i = 0;

@SuppressWarnings("resource")
public static void main(String[] args) {
// TODO Auto-generated method stub
MyThread_s my = new MyThread_s();
my.start();

while (true) {
System.out.println("1.存钱  2.取钱  3.查询余额");
int num = new Scanner(System.in).nextInt();
if (num == 1) {
Mythread();
Mythread();
System.out.print("存入数(张)：");
int num_CR = new Scanner(System.in).nextInt();
i += num_CR * 100;
} else if (num == 2) {
Mythread();
Mythread();
System.out.print("取出数(张)：");
int num_QC = new Scanner(System.in).nextInt();
if (num_QC > i / 100)
System.out.println("余额不足！");
else if (num_QC < 0) {
main(args);
} else {
i -= num_QC * 100;
}
} else if (num == 3) {
Mythread();
Mythread();
System.out.print("余额：" + i+"元！");
} else {
main(args);
}
}
}

public static void Mythread() {

new Thread() {
@Override
public void run() {
// TODO Auto-generated method stub
}
}.start();

}
}
