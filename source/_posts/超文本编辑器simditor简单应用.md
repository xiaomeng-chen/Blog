---
title: 超文本编辑器simditor简单应用

tags: javascript

categories: 笔记

---

我正在做一个在线考试的网站，那就需要老师布置试题，但是麻烦的是试题里面可能会有图片，答案里面也可能要有图片，所以就很麻烦，这时候想到了富文本编辑器，于是就发现了simditor，功能比较简单，加载也比较快
http://www.jq22.com/jquery-info590

```html
<div class="am-g">
    <div class="am-u-md-6 am-cf">
        <div class="am-fl am-cf">
            <div class="am-btn-toolbar am-fl">
                <div class="am-btn-group am-btn-group-xs">
                    <button type="button" class="am-btn am-btn-default" id="b0"><span class="am-icon-plus"></span> 编辑题目</button>
                </div>
                <div class="am-btn-group am-btn-group-xs">
                    <button type="button" class="am-btn am-btn-default" id="b1"><span class="am-icon-plus"></span> A选项</button>
                </div>
                <div class="am-btn-group am-btn-group-xs">
                    <button type="button" class="am-btn am-btn-default" id="b2"><span class="am-icon-plus"></span> B选项</button>
                </div>
                <div class="am-btn-group am-btn-group-xs">
                    <button type="button" class="am-btn am-btn-default" id="b3"><span class="am-icon-plus"></span> C选项</button>
                </div>
                <div class="am-btn-group am-btn-group-xs">
                    <button type="button" class="am-btn am-btn-default" id="b4"><span class="am-icon-plus"></span> D选项</button>
                </div>      
            </div>          
        </div>

    </div>
    <form class="am-form am-form-inline" style="display:inline-block;height:30px">
        <div class="am-form-group " style="margin-bottom: 0">
            <input type="number" id="score" placeholder="请输入分值" required>
        </div>
        <div class="am-form-group " style="margin-bottom: 0;width: 100px">
            <select  required  id="answer">
                <option value="A">A</option>
                <option value="B">B</option>
                <option value="C">C</option>
                <option value="D">D</option>
            </select>
            <span class="am-form-caret"></span>
        </div>
    </form>
</div>
<br/>
<div class="am-g">
    <div class=" am-u-sm-centered">
        <textarea rows="5" placeholder="请输入内容" id="editor" autofocus></textarea>
        <br/>
        <button type="button" id="submit" class="am-btn am-btn-primary am-radius" style="position: absolute;right: 5%;bottom: 0">提交</button>
    </div>
</div>
```
html主要代码如上，下面介绍一下simditor的用法
```html
<!--首先在网页中引用css和js文件-->
<link href="~/Scripts/bower_components/fontawesome/css/font-awesome.css" rel="stylesheet" />
<link href="~/Scripts/bower_components/simditor/styles/simditor.css" rel="stylesheet" />
<link href="~/Scripts/bower_components/simditor-emoji/styles/simditor-emoji.css" rel="stylesheet" />

<script src="/Scripts/bower_components/jquery/dist/jquery.min.js"></script>
<script src="~/Scripts/bower_components/simple-module/lib/module.js"></script>
<script src="~/Scripts/bower_components/simple-hotkeys/lib/hotkeys.js"></script>
<script src="~/Scripts/bower_components/simple-uploader/lib/uploader.js"></script>
<script src="~/Scripts/bower_components/simditor/lib/simditor.js"></script>
<script src="~/Scripts/bower_components/simditor-emoji/lib/simditor-emoji.js"></script>
<script src="~/Scripts/bower_components/simditor-markdown/lib/simditor-markdown.js"></script>
```
接着初始化编辑器
```html
<script>
    var editor = new Simditor({
        textarea: $('#editor'),
        toolbar: [
            'title',
            'bold',
            'underline',
            'strikethrough',
            'color',
            'ol', 'ul',
            'blockquote',
            'code',
            'table',
            'link',
            'image',
            'hr',
            'indent', 'outdent',
            'emoji'
        ],
        upload: {
            'url': '/Common/Upload/Index',

                'connectionCount': 8
            },
            pasteImage: true,
            emoji: {
                imagePath: '/Scripts/bower_components/simditor-emoji/images/emoji/'
            },
            markdown: true
        });
</script>
```
这样编辑器就可以使用了，下面是一些编辑试题的逻辑
```html
 <script>
        $(function () {
            var t = $("#editor");
            var t0 = [];
            var t1 = [];
            var t2 = [];
            var t3 = [];
            var t4 = [];
            var score = $("#score");
            var trueop =$("#answer");
            var nowT = t0;
            $("#b0").click(function () {
                nowT[0]= t.val();
                nowT = t0;
                editor.setValue(t0);
            });
            $("#b1").click(function () {
                nowT[0] = t.val();
                nowT = t1;
                editor.setValue(t1);
            });
            $("#b2").click(function () {
                nowT[0] = t.val();
                nowT = t2;
                editor.setValue(t2);
            });
            $("#b3").click(function () {
                nowT[0] = t.val();
                nowT = t3;
                editor.setValue(t3);
            });
            $("#b4").click(function () {
                nowT[0] = t.val();
                nowT = t4;
                editor.setValue(t4);
            });
            $("#submit").click(function () {
                nowT[0] = t.val();
                if (t0 == [""]) {
                    alert("题目不能为空");
                }
                else if (t1 == [""]) {
                    alert("A选项不能为空");
                }
                else if (t2 == [""]) {
                    alert("B选项不能为空");
                }
                else if (t3 == [""]) {
                    alert("C选项不能为空");
                }
                else if (t4 == [""]) {
                    alert("D选项不能为空");
                }
                else if (score.val()==0) {
                    alert("分值不能为空");
                }
                else if (trueop.val() == [""]) {
                    alert("答案不能为空");
                } else {
                    $.ajax({
                        url: "/Admin/Questions/AddTest",
                        data: {
                            content: t0[0],
                            aop: t1[0],
                            bop: t2[0],
                            cop: t3[0],
                            dop: t4[0],
                            correctop: trueop.val(),
                            score: score.val()
                        },
                        success: function (res) {
                            if (res == 0) {
                                alert("添加失败");
                            } else {
                                alert("成功");
                                window.location.href = "/Admin/Questions/Add";
                            }
                        }
                        
                    });
                }
                
            });

        });
    </script>
```

自此终于搞定了这个问题，这个过程用到了一些东西，ajax，simditor，还有文件上传，通过一步步的调试，改bug，越来越熟练网页的开发，没发现simditor之前本来还天真的想自己解决这个问题，既然有成熟的插件，就要学会去用，这样不只会节省时间，而且效果也非常好。




