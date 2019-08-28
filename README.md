# fe-learning-summary

作为一名在前端行业工作不久的程序员，想把自己在工作学习中遇到的问题记录下来。

# 动态设置iframe高度

场景是：在父窗口中根据iframe里面的内容动态修改iframe的高度。

###### 解决方案如下：

(1)页面布局
```
<div >
    <iframe src="test.html" id="js-iframe" width="780px" height="330px" frameborder='0' scrolling='0'></iframe>
</div>
```
(2)js操作

```
/*
*其中'#js-iframe'为iframe的id,'.js-btn'、'.content'为iframe里面的元素类名；
*此处主要是点击iframe里面的按钮可展示的内容不一样，所以所需要的高度也不同，从而需要动态设置iframe的高度；
等iframe加载完之后，在监听点击事件，然后获取相应的iframe里面内容的高度，再将获取到的高度设置到iframe上。
*/

$("#js-iframe").on('load', function() {
    $($("#js-iframe")[0].contentDocument.body).on('click', '.js-btn', function() {
        //此处为操作iframe里元素的代码
        var contentHeight = $("#js-iframe").contents().find("body").find(".content").height();
        $("#js-iframe").height(contentHeight);
    });
});
```

# 测试test

