---
layout: post
title: "java连接mysql数据库实现增删改查"
date: 2018-3-10 20:33
description: "java连接mysql数据库实现增删改查"
tag: java
---

今天带大家实现java连接mysql数据库实现增删改查，准备工具[eclipse](http://www.eclipse.org/downloads/packages/eclipse-ide-java-developers/oxygen2)、[MySQL数据库](https://dev.mysql.com/downloads/installer/)、[mysql-connector-java-5.1.39-bin.jar](https://pan.baidu.com/s/1xcw2c2sxyiX1Yf4mCFM_qw)密码：v4gr，一切准备完毕后开始编码操作.
数据库设计如下：
<div align="center">
<img src="/images/image/MYSQL.png" height="500" width="500" />
</div>



```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;

import com.mysql.jdbc.Statement;

public class Mysql {
	final static String JDBC_DRIVER = "com.mysql.jdbc.Driver";
	final static String DB_URL = "jdbc:mysql://127.0.0.1:3360/user";

	final static String USER = "xiaopihaier";
	final static String PASS = "1234567890.";

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Statement stmt = null;

		try {
			Class.forName(JDBC_DRIVER);
			System.out.print("连接数据库中......");
			Connection conn = DriverManager.getConnection(DB_URL, USER, PASS);

			System.out.print("事例化对象'''''");
			stmt = (Statement) conn.createStatement();
			String sql;
			sql = "SELECT id ,username,password FROM userinform";
			ResultSet rs = stmt.executeQuery(sql);

			while (rs.next()) {
				int id = rs.getInt("id");
				String name = rs.getString("username");
				String password = rs.getString("password");

				System.out.println("id:" + id);
				System.out.println("username" + name);
				System.out.println("password" + password);
				System.out.println("\n");
			}

			rs.close();
			stmt.close();
			conn.close();
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

	}

}

```
