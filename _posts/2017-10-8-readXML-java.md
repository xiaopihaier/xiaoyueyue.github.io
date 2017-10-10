---
layout: post
title: "JavaXML解析"
date: 2017-10-8 21:14
description: "JavaXML解析"
tag: java
---


今天来实现一个Java解析一个xml的网站，看看效果是啥样的


```
package com.xiaopihaer;
import java.io.File;
import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import org.w3c.dom.Document;
import org.w3c.dom.Element;
import org.w3c.dom.Node;
import org.w3c.dom.NodeList;

public class ReadXML {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		try {
			DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
			DocumentBuilder builder = factory.newDocumentBuilder();
			Document document = builder.parse(new File("languages.xml"));
			Element root = document.getDocumentElement();
			System.out.println("cat=" + root.getAttribute("cat"));
			NodeList list = root.getElementsByTagName("lan");
			for (int i = 0; i < list.getLength(); i++) {
				Element lan = (Element) list.item(i);
				System.out.println("---------------------");
				System.out.println("id=" + lan.getAttribute("id"));

				NodeList clist = lan.getChildNodes();
				for (int j = 0; j < clist.getLength(); j++) {
					Node c = clist.item(j);
					if (c instanceof Element) {
						System.out.println(c.getNodeName() + "=" + c.getTextContent());
					}
				}
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}
```
