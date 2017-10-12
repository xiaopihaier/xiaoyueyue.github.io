---
layout: post
title: "Android通过服务器验证用户名和密码"
date: 2017-10-10 15:00
description: "Android通过服务器验证用户名和密码"
tag: Android
---


前面跟大家讲解了如何射击一个自己设计的精美登陆界面，今天就带大家实现登陆和后台实现登陆的验证。
第一步：
准备工具如下：模拟器任意，WindowsServer2008R2，sqlserver2012，Java编译环境，Javaee编译器（eclipse）
第二步骤：
服务端，我们先创建一个数据库，叫做Menu，然后我们再在数据库中创建一个表，叫做LoginInformation,表中我们创建两个字段，一个username，一个password，如图所示设置。
<div align="center">
	<img src="/images/image/SQLServer.png" height="800" width="500" />
</div>
随后我们创建一个javaweb，用来处理客户端向服务端发送的数据，这里要用到sqljdbc4.jar文件，将此文件放入WebContent-WEB-INF-lib目录下，随后我们创建两个jsp文件用于实现客户端的注册和登陆，并返回json数据，Android客户端解析jsp返回的json数据。

注册检测代码如下：

```
<%@page import="java.util.HashMap"%>
<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.Statement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%
	try {
		boolean flag = false;//登陆状态
		request.setCharacterEncoding("UTF-8");
		String username = request.getParameter("username");
		String password = request.getParameter("password");
		Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");//加载数据库驱动,注册到驱动管理器
		String url = "jdbc:sqlserver://localhost:1433;DatabaseName=Menu";//数据库连接字符串
		String username_sql = "xiaopihaier";//数据库用户名
		String password_sql = "BaBy520.";//数据库密码
		//创建connection连接
		Connection conn = DriverManager.getConnection(url, username_sql, password_sql);
		// 创建statement 负责执行sql语句
		Statement st = (Statement) conn.createStatement();
		ResultSet rs = (ResultSet) st.executeQuery("SELECT * FROM LoginInformation");
    JSONObject jb = new JSONObject();
		if (conn != null) {
			while (rs.next()) {// 指向下一行数据 如何有数据返回TRUE 没数据返回FALSE
				if (username.equals(rs.getString("username"))) {
					flag = true;
				}
			}
		}
		if (flag) {
      out.println(jb.put("Result", "用户名已被使用"));
		} else {
			// 插入数据
			st.executeUpdate("insert into LoginInformation(username,password) values(" + username + ","
					+ password + ")");
      out.println(jb.put("Result", "注册成功"));
		}
	} catch (Exception e) {
		e.printStackTrace();
	}
%>
```

登陆测试代码：
```
<%@page import="org.json.JSONObject"%>
<%@page import="java.util.ArrayList"%>
<%@page import="java.sql.ResultSet"%>
<%@page import="java.sql.Statement"%>
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.Connection"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%
	try {
		boolean flag = false;
		request.setCharacterEncoding("UTF-8");
		String username = request.getParameter("username");
		String password = request.getParameter("password");
		Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");//加载数据库驱动,注册到驱动管理器
		String url = "jdbc:sqlserver://localhost:1433;DatabaseName=Menu";//数据库连接字符串
		String username_sql = "xiaopihaier";//数据库用户名
		String password_sql = "BaBy520.";//数据库密码
		//创建connection连接
		Connection conn = DriverManager.getConnection(url, username_sql, password_sql);
		// 创建statement 负责执行sql语句
		Statement st = (Statement) conn.createStatement();
		ResultSet rs = (ResultSet) st.executeQuery("SELECT *FROM LoginInformation");
		JSONObject jb = new JSONObject();
		if (conn != null) {
			while (rs.next()) {// 指向下一行数据 如何有数据返回TRUE 没数据返回FALSE
				if (username.equals(rs.getString("username")) && (password.equals(rs.getString("password")))) {
					flag = true;
				}
			}
		}
		if (flag) {
			out.println(jb.put("Result", "登陆成功"));
		} else {
			out.println(jb.put("Result", "用户名或密码错误"));
		}
	} catch (Exception e) {
		e.printStackTrace();
	}
%>
```

第二步：
我们服务端创建好后开始动手我们的客户端，我们来看看Login.java文件的代码：

```
package com.example.xiaopihaier.menu;

import android.os.AsyncTask;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.support.v7.app.AppCompatActivity;
import android.text.TextUtils;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import org.json.JSONException;
import org.json.JSONObject;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URL;
import java.net.URLConnection;

public class Login extends AppCompatActivity implements View.OnClickListener {

    EditText username, password;
    Button login;
    StringBuilder stringBuilder;
    String line, msg, result;
    static final int UPDATE_TEXT = 1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);
        init();
    }

    private Handler handler = new Handler() {
        public void handleMessage(Message message) {
            switch (message.what) {
                case UPDATE_TEXT:
                    Toast.makeText(Login.this, "登陆成功", Toast.LENGTH_LONG).show();
                    break;
                default:
                    break;
            }
        }
    };

    private void init() {
        username = (EditText) findViewById(R.id.Username);
        password = (EditText) findViewById(R.id.Password);
        login = (Button) findViewById(R.id.Login);
        login.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.Login:
                if (TextUtils.isEmpty(username.getText().toString().trim())) {
                    Toast.makeText(Login.this, "请输入用户名", Toast.LENGTH_LONG).show();
                } else if (TextUtils.isEmpty(password.getText().toString().trim())) {
                    Toast.makeText(Login.this, "请输入密码", Toast.LENGTH_LONG).show();
                } else {
                    Get();
                }
                break;
            default:
                break;
        }
    }

    private void Get() {
        new AsyncTask<String, Void, Void>() {
            @Override
            protected Void doInBackground(String... params) {
                try {
                    URL url = new URL(params[0]);
                    URLConnection connection = url.openConnection();
                    InputStream inputStream = connection.getInputStream();
                    InputStreamReader inputStreamReader = new InputStreamReader(inputStream, "utf-8");
                    BufferedReader bufferedReader = new BufferedReader(inputStreamReader);
                    stringBuilder = new StringBuilder();
                    while ((line = bufferedReader.readLine()) != null) {
                        stringBuilder.append(line);
                    }
                    bufferedReader.close();
                    inputStreamReader.close();
                    inputStream.close();
                    Json();
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return null;
            }
        }.execute("http://www.xiaopihaier.top/AndroidApi/login.jsp?username=" + username.getText().toString().trim() + "&password=" + password.getText().toString().trim());
    }

    private void Json() {
        try {
            JSONObject jsonObject1 = new JSONObject(stringBuilder.toString());
            msg = jsonObject1.optString("Result");
            Log.i("msg", msg);
        } catch (JSONException e) {
            e.printStackTrace();
        }
    }

}
```

别忘了再在AndroidManifest.xml文件中添加一个网络权限:```<uses-permission android:name="android.permission.INTERNET"/>```

最后附上运行结果图：
<div align="center">
	<img src="/images/image/msg.png" height="200" width="300" />
</div>
