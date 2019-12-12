# JQuery上传图片

### 1、采用form表单上传

```
<form action="/upload" method="post" enctype="multipart/form-data">
    <input type="file" name="file"/>
    <input type="submit" value="提交"/>
</form>

```

### 2、采用ajax上传

#### 方法一：

##### html结构：
```
<input type="file" name="file" onchange="getPhoto(this)" accept="image/gif,image/jpeg,image/jpg,image/png,image/svg"/>
```

##### 采用ajax上传：
```
// 上传照片
window.getPhoto = function(node) {
    var formData = new FormData();
    formData.append("file", node.files[0]);
    $.ajax({
        url : "/upload/picture",
        type : "POST",
        data : formData,
        cache:false,
        contentType: false,
        processData:false,
        success : function(result) {
            if (result.status === 0) {
                
            } else {
                
            }
        }
    });

}
```

#### 方法二：

##### html结构：
```
<form method="post" enctype="multipart/form-data" class="uploadForm">
    <input type="file" name="file" onchange="getPhoto(this)" accept="image/gif,image/jpeg,image/jpg,image/png,image/svg"/>
</form>
```

##### 采用ajax上传：
```
// 上传照片
window.getPhoto = function(node) {
    var formData = new FormData($('.uploadForm')[0]);
    $.ajax({
        url : "/upload/picture",
        type : "POST",
        data : formData,
        cache:false,
        contentType: false,
        processData:false,
        success : function(result) {
            if (result.status === 0) {
                
            } else {
                
            }
        }
    });

}
```
### 注意事项

- processData设为false。因为data值为FormData对象，不需要对数据做处理；
- 如果是form表单直接提交，标签需添加enctype="multipart/form-data"属性；
- cache设置为false，上传文件不需要缓存；
- contentType设置为false，因为由表单构造的FormData对象，且已经声明了属性enctype="multipart/form-data"，所以这里设置为false。