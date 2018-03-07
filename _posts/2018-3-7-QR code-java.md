---
layout: post
title: "java使用zxing包实现二维码生成"
date: 2018-3-7 23:05
description: "java使用zxing包实现二维码生成"
tag: java
---


今天带大家来实现自己的二维码生成，首先我们要准备一个[zxing.jar](https://pan.baidu.com/s/1qCXbYtZi-aHHaItqXjplCQ)包,密码：4hk4;现在我们创建一个Java工程，然后创建一个lib文件夹，将下载的jar包放入lib文件夹然后导入到工程中，现在创建我们的主体代码，代码如下：

```
package zxing;

import java.io.File;
import java.nio.file.Path;
import java.util.HashMap;
import com.google.zxing.BarcodeFormat;
import com.google.zxing.EncodeHintType;
import com.google.zxing.MultiFormatWriter;
import com.google.zxing.client.j2se.MatrixToImageWriter;
import com.google.zxing.common.BitMatrix;
import com.google.zxing.qrcode.decoder.ErrorCorrectionLevel;

public class CreatQRCode {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int width = 300;
		int height = 300;
		String format = "png";
		String content = "试验";

		// 定义二维码参数
		HashMap hashmap = new HashMap();
		hashmap.put(EncodeHintType.CHARACTER_SET, "utf-8");// 设置字符集
		hashmap.put(EncodeHintType.ERROR_CORRECTION, ErrorCorrectionLevel.M);// 设置纠错级别
		hashmap.put(EncodeHintType.MARGIN, 2);// 设置空白区域大小

		// 生成二维码
		try {
			BitMatrix bitmatrix = new MultiFormatWriter().encode(content, BarcodeFormat.QR_CODE, width, height,
					hashmap);
			Path file = new File("C:/img.png").toPath();
			MatrixToImageWriter.writeToPath(bitmatrix, format, file);
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

	}
}
```

完成后查看电脑C盘是否出现一个叫img.png的文件，如果有说明创建二维码成功，打开图片使用手机扫描，看看是否为自己的文字。最后贴上自己实验的结果：
<div align="center">
<img src="/images/image/QR Code.png" height="100" width="100" />
	<img src="/images/image/QR Code_Results.png" height="100" width="100" />
</div>
