# v-cloak

> 解决页面加载时出现闪烁。

具体用法：v-cloak并不需要添加到每个标签，只要在el挂载的标签上添加就可以。

```
<div class="#app" v-cloak>
    <p>{{value.name}}</p>
</div>
```
在css中添加：
```
[v-cloak] {
    display: none;
}
```

