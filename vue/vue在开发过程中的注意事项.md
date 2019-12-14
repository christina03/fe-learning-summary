# Vue在开发过程中的注意事项

### 1、为列表渲染设置属性key

key这个属性主要用在Vue.js的虚拟DOM算法中，在对比新旧虚拟节点时辨识虚拟节点。

### 2、在v-if/v-if-else/v-else中使用key

### 3、路由切换组件不变

在使用Vue.js时，当页面切换到同一个路由但不同参数的地址时，组件的生命周期钩子并不会重新触发。

解决方法如下：
- （1）路由导航守卫beforeRouteUpdate：只需要把每次切换路由时需要执行的逻辑放到beforeRouteUpdate守卫中即可。
- （2）在watch中添加观察$route对象的变化
- （3）为router-view组件添加属性key：该方法非常简单粗暴，每次切换路由时都会被销毁并且重新创建，非常浪费性能。

### 4、为所有路由统一添加query

- （1）使用全局守卫beforeEach：该方法并不具备修改query的能力，但可以再其中使用next方法来中断当前导航，并切换到新导航，添加一些新的query进去。

优点：可以全局统一配置公共的query参数，并且组件内切换路由时无须进行特殊处理。

缺点：每次切换路由时，全局守卫beforeEach会执行两次，即每次切换路由其实是切换两次。

- （2）使用函数劫持：通过拦截router.history.transitionTo方法，在vue-router内部在切换路由之前将参数添加到query中。

优点：可以全局添加query参数并不会导致路由切换两次。

缺点：通过修改vue-router内部方法实现目的，这是一种危险操作。

### 5、避免v-if和v-for一起使用

- 为了过滤一个列表中的项目，请将列表替换成一个计算属性，返回过滤后的列表。
- 为了避免渲染本应该被隐藏的列表，请将v-if移动至容器元素上。

### 6、为组件设置样式作用域

- 通过设置scoped特性
- 通过设置CSS Module特性

```
<template>
    <button :class="[$style.button, $style.buttonClose]">X</button>
</template>
<style module>
    .button{
        border:none;
    }
    .buttonClose{
        color:red;
    }
</style>
```
