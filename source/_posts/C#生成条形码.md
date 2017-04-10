---
title: C#生成条形码

tags: C# 笔记

categories: code

---
首先在程序中添加zxing包
```C#
 using  zxing;
```
```C#
EncodingOptions op = new EncodingOptions();
op.Width = 400;
op.Height = 200;
BarcodeWriter writer = new BarcodeWriter();
writer.Options = op;
writer.Format = BarcodeFormat.CODE_39;

Bitmap img = writer.Write(s);

//自动保存图片到当前目录
string fullUrl = dic+"\\";
if (Directory.Exists(fullUrl) == false)
{
    Directory.CreateDirectory(fullUrl);   
    //如果文件夹不存在，直接创建文件夹。
}
var filename = fullUrl + name+ ".jpg";
img.Save(filename, ImageFormat.Jpeg);


```
           


