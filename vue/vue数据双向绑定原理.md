# vue数据双向绑定原理

```
<input v-model="inputMsg">
// 两者等价
<input :value="inputMsg" @input="inputMsg = $event.target.value">
```
- `$event`指代当前触发的事件对象
- `$event.target`指代当前触发的事件对象的dom
- `$event.target.value`指代当前触发的事件对象dom的值
