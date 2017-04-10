---
title: OpenXml 操作Word Excel

tags: C#

categories: code

---
下面是两篇参考博客
Word ：http://blog.csdn.net/francislaw/article/details/7568317
Excel ：http://www.cnblogs.com/BeyondWJsel/archive/2012/05/10/2494418.html

由于项目需要，我只学习了word插入文字部分，剩下的需要再回来看

```C#
//在word对应的mark位置插入文字
public void bookmark(WordprocessingDocument file, string markname, string str)
    {
        Dictionary<String, BookmarkStart> bookmarkMap =
        new Dictionary<String, BookmarkStart>();

        foreach (BookmarkStart bookmarkStart in file.MainDocumentPart.RootElement.Descendants<BookmarkStart>())
            {
                if (bookmarkStart.Name == markname)
                {
                    var run = new Run();
                    run.Append(new Text(str));
                    bookmarkStart.InsertAfterSelf(run);
                }
            }

            //foreach (BookmarkStart bookmarkStart in bookmarkMap.Values)
            //{
            //    var run = new Run();
            //    run.Append(new Text("Hello World"));
            //    bookmarkStart.InsertAfterSelf(run);         
            //}
    }
```

```C# 
//打开一个word插入文字
public static void AddString(string filePath, string str)
    {
            using (WordprocessingDocument doc = WordprocessingDocument.Open(filePath, true))
            {
                Paragraph paragraph = new Paragraph();
                Run run = new Run();

                RunProperties runProperties = new RunProperties(); //属性

                //RunFonts fonts = new RunFonts() { EastAsia = "DFKai-SB" }; // 设置字体
                //FontSize size = new FontSize() { Val = "52" }; // 设置字体大小
                //Color color = new Color() { Val = "red" }; // 设置字体样式

                // 将样式添加到属性里面
                //runProperties.Append(color);
                //runProperties.Append(size);
                //runProperties.Append(fonts);

                //run.Append(runProperties);
                run.Append(new Text(str));
                paragraph.Append(run);
                doc.MainDocumentPart.Document.Body.Append(paragraph);
                doc.MainDocumentPart.Document.Save();
            }
    }
```
```C#
//根据文字新建word
public void Create(string filePath, string str)
    {
    var psth = Server.MapPath(@"~/Word");
    using (WordprocessingDocument doc = WordprocessingDocument.Create(psth + "\\t.docx", WordprocessingDocumentType.Document))
        {
            // ②：为doc添加MainDocumentPart部分  
            MainDocumentPart mainPart = doc.AddMainDocumentPart();

            // ③：为mainPart添加Document，对应于Word里的文档内容部分  
            mainPart.Document = new Document();

            // ④：为Document添加Body，之后所有于内容相关的均在此body中  
            Body body = mainPart.Document.AppendChild(new Body());

            // ⑤：添加段落P，P中包含一个文本“TEST”  
            Paragraph p = mainPart.Document.Body.AppendChild(new Paragraph());
            p.AppendChild(new Run(new Text("TEST")));
        }
    }

```




