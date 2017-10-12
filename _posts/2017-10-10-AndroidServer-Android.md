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
服务端，我们先创建一个数据库，叫做Menu，然后我们再在数据库中创建一个表，叫做LoginInformation,表中我们创建两个字段，一个username，一个password，如图所示设置。随后我们创建一个javaweb，用来处理客户端向服务端发送的数据，这里要用到sqljdbc4.jar文件，将此文件放入WebContent-WEB-INF-lib目录下，随后我们创建两个jsp文件用于实现客户端的注册和登陆。

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
		if (conn != null) {
			while (rs.next()) {// 指向下一行数据 如何有数据返回TRUE 没数据返回FALSE
				if (username.equals(rs.getString("username"))) {
					flag = true;
				}
			}
		}
		if (flag) {
			out.println("用户名已被使用");
		} else {
			// 插入数据
			st.executeUpdate("insert into LoginInformation(username,password) values(" + username + ","
					+ password + ")");
			out.println("注册成功");
		}
	} catch (Exception e) {
		e.printStackTrace();
	}
%>
```

登陆测试代码：
```
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
		if (conn != null) {
			while (rs.next()) {// 指向下一行数据 如何有数据返回TRUE 没数据返回FALSE
				if (username.equals(rs.getString("username")) && (password.equals(rs.getString("password")))) {
					flag = true;
				}
			}
		}
		if (flag) {
			out.println("登陆成功");
		} else {
			out.println("用户名或密码错误");
		}
	} catch (Exception e) {
		e.printStackTrace();
	}
%>
```
