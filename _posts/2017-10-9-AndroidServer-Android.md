---
layout: post
title: "制作Android自定义登陆窗口"
date: 2017-10-9 20:05
description: "制作Andoird自定义登陆窗口"
tag: Android
---

做过Android开发的都知道Android自带的登陆界面那是真的惨不忍睹，so，今天就带大家来实现自定义的Android登陆界面。
看起来绝对是让自己和用户满意的。

第一步：
我们开始还是要创建一个初始的登陆界面，尽管看起来是那么的丑陋，没事，我们慢慢的修改，慢慢的给他化妆，让他变得美美哒o(*￣▽￣*)ブ
<div align="center">
	<img src="/images/image/Login.jpg" height="500" width="500" />
  </div>
可能大叫都会想：这人是不是在骗我们啊，这界面明明这么丑，说好的美美哒的界面呢，(╯▔皿▔)╯。在这儿，我给各位看官说说，你们放心
我不会骗大家的，这只是第一步，后面还要继续呢。最后我们大家都来看看效果，就知道我有没有骗大家哦~~~///(^v^)\\\~~~
第二步：
开始我们的修改，这就是修改完成后的效果图，是不是比原来的要好看多了，没骗你们吧，后面附上相关的代码片段供大家学习和参考，也许你们
也可以比我做的更好也说不定呢。


login.xml文件中的代码如下：
```
    <LinearLayout
        android:layout_width="300dp"
        android:layout_height="300dp"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="60dp"
        android:background="@drawable/background_from1"
        android:orientation="vertical">

        <EditText
            android:layout_width="220dp"
            android:layout_height="50dp"
            android:layout_above="@+id/Password"
            android:layout_gravity="center"
            android:layout_marginTop="20dp"
            android:background="@drawable/background_edit"
            android:gravity="center"
            android:hint="@string/Username"
            android:inputType="number"
            android:textColor="@color/color_text"/>

        <EditText
            android:id="@+id/Password"
            android:layout_width="220dp"
            android:layout_height="50dp"
            android:layout_gravity="center"
            android:layout_marginTop="20dp"
            android:background="@drawable/background_edit"
            android:gravity="center"
            android:hint="@string/Password"
            android:inputType="numberPassword"
            android:textColor="@color/color_text"/>

        <Button
            android:id="@+id/Login"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_marginTop="20dp"
            android:background="@drawable/background_button"
            android:gravity="center"
            android:text="@string/Login"
            android:textColor="@color/color_text"
            android:textSize="20sp"
            android:textStyle="bold"/>
    </LinearLayout>
```
登陆按钮的样式代码如下：
```
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="#0f50cec1"/>
    <corners
        android:bottomLeftRadius="10dp"
        android:bottomRightRadius="10dp"
        android:topLeftRadius="10dp"
        android:topRightRadius="10dp"
        />
</shape>
```

输入框的样式代码：
```
<shape xmlns:android="http://schemas.android.com/apk/res/android"
       android:shape="rectangle">
    <solid android:color="#2fe7e7b4"/>
    <stroke
        android:width="1dp"
        android:color="#2fffffff"/>
    <corners
        android:bottomLeftRadius="8dp"
        android:bottomRightRadius="8dp"
        android:topLeftRadius="8dp"
        android:topRightRadius="8dp"/>
</shape>
```

中间半透明效果的方框代码如下：
```
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="#0ffdfdfd"/>
    <corners
        android:bottomLeftRadius="10dp"
        android:bottomRightRadius="10dp"
        android:topLeftRadius="10dp"
        android:topRightRadius="10dp"
        />
</shape>
```
