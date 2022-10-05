---
title: Ajax实现文件上传
tags:
  - 前端
  - Ajax
categories: 前端
abbrlink: 36363
date: 2021-05-05 18:35:51
---
# 1.前端demo
```
<script type="text/javascript">
    function btnSubmit() {
        var img = document.getElementById('images').files[0];
        var fd = new FormData();
        fd.append('FILE', img);
        fd.append('name', 'xiaoming');
        $.ajax({
            type: "post",
            url: "http://127.0.0.1/test.php",
            processData: false,//非常重要，不可省略
            contentType: false,//非常重要，不可省略
            dataType: "json",
            data: fd,
            success: function(data) {

            },
            error: function(data) {

            }
        });
    }
</script>
```
# 2.服务端demo
```
$imgName=$_FILES['FILE']['name'];
$tmp_name=$_FILES['FILE']['tmp_name'];
$fileName='./123.jpg';
$rst=move_uploaded_file($tmp_name,$fileName);
echo $rst;
```
注：
1.$fileName路径中的路径必须存在；
2.$fileName路径中不可出现中文；
若不满足则两种情况，可能会false；