---
layout: post
title: "AndoridMD5实现密码加密"
date: 2017-10-14 09:46
description: "AndoridMD5实现密码加密"
tag: Android
---

前面我们实现了客户端和服务器的远程通信，用来实现登陆界面的注册和登陆测试。你们是不是也发现了问题的存在啦，就是我们的
密码都是明文上传给服务器的，要是别人截取到通信不就知道我们的密码了么，想想是不是很恐怖😱。今天我们就来实现密码的加密
处理，防止这种恐怖的事情发生。我们打开AndroidStudio编译器，打开工程找到Login.java文件，我们先定义一个String类型的
变量：password_MD5。随后我们找到Get();方法，我们在try下面创建一个MD5();方法。
具体实现如下代码所示：
```
private void Get() {
        new AsyncTask<String, Void, Void>() {
            @Override
            protected Void doInBackground(String... params) {
                try {
                    MD5();
                    URL url = new URL(params[0]);
              ...
    }
```
到这儿开始实现我们的MD5方法了,放上具体的代码：
```
private void MD5() {
       try {

           MessageDigest MD5 = MessageDigest.getInstance("MD5");

           MD5.update(password.getText().toString().getBytes(), 0, password.getText().toString().length());

           Log.i("password加密前：",password.getText().toString());

           password_MD5=new BigInteger(1, MD5.digest()).toString(16);

           Log.i("password加密后：",password_MD5);

       } catch (Exception e) {

           e.printStackTrace();
       }

   }
```
最后我们将Git();方法中url链接地址改为注册的链接地址且将passowrd改为password_MD5。我们就用注册接口来看看我们加密后的效果吧:
<div align="center">
	<img src="/images/image/passwordMD5.png" height="100" width="100" />
  <img src="/images/image/passwordMD5_sql.png" height="100" width="300" />
</div>
到此说明我们的加密成功了，连数据库的管理员都不知道你的密码啦。
