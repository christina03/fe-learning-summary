# Vue.use与Vue.prototype.$XXX的用法区别

### 1、Vue.use

通过`Vue.use`引入插件，可以理解为自己定义的方法或者引入的Element-ui组件。

当`vue.use`引入了Element-ui之后，可以通过`this.$xxx`调用该方法。

- Vue的插件是一个对象，如Element
- 插件对象必须有install字段
- install对象是一个函数
- 初始化插件对象需要通过Vue.use()

### 2、Vue.prototype.$xxx

如下代码，通过Vue.prototype.$util，就可以在任意组件内部运行this.$utils()了。
```
import utils from '@/pages/util/utils'
Vue.prototype.$util=utils 
```
每一个vue组件都是Vue的实例，所以组件内this可以拿到Vue.prototype上添加的属性和方法。

当在很多组件里用到数据/实例工具，但是不想污染全局作用域，这时可以通过在原型上定义它们，使其在每个Vue实例中可用。
