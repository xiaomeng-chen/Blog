---
title: C#特性

tags: C#

categories: code

---

```C#
    ///获取myclass的特性
    System.Reflection.MemberInfo info = typeof(MyClass);
    object[] attributes = info.GetCustomAttributes(true);
    for (int i = 0; i < attributes.Length; i++)
    {
             System.Console.WriteLine((attributes[i] as             HelpAttribute).Url);
    }
```




