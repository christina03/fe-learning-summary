# JS基础知识

### 1、typeof返回值有哪些？

```
typeof undefinded  //undefined
typeof 'abc' //string
typeof true //boolean
typeof 100 //number
typeof [] //object
typeof {} //object
typeof null //object
typeof console.log //function
//es6里面还有 symbol类型
```
### 2、js中的内置函数

> js中有哪些内置函数——数据封装类对象

- Object
- Array
- Boolean
- Number
- String
- Function
- Date
- RegExp
- Error

> js按存储方式区分变量类型

- 值类型：String\Number\Boolean\undefinded
- 引用类型:Object/Array/Function/null

> 如何理解JSON，它是一个对象,也是一种数据格式

- JSON.stringify()
- JSON.parse()

### 3、instanceof

使用instanceof判断一个函数是否是一个变量的构造函数。

> 用于判断引用类型的函数属于哪个构造函数。

示例：f instanceof Foo:表示f的__proto__一层一层往上找，能否找到对应的Foo.prototype。

### 4、原型

#### 5大原型规则

- 所有的引用类型（数组、对象、函数），都具有对象特性，即可自由扩展属性（null除外）。
- 所有的引用类型（数组、对象、函数），都有一个__proto__属性，属性值是一个普通的对象（null除外）。
- 所有函数，都有一个prototype属性，属性值是一个普通函数。
- 所有的引用类型（数组、对象、函数），__proto__属性值指向它的构造函数的“prototype”属性值。
- 当试图得到一个对象的某个属性时，如果这个对象本身没有这个属性，那么会去它的__proto__(即它的构造函数的prototype)中寻找。

#### 原型链

.toString()（.__proto__.__proto__）

![原型链](https://note.youdao.com/yws/api/personal/file/WEB6b6206ff17becce03eb23245ef448f98?method=download&shareKey=3a07a2057de8b978cafab4b7af59dc1b)

#### 5、作用域

- js没有块级作用域，只有函数和全局作用域。
- ES6有块级作用域。

this要在执行时才能确认值，定义时无法确认。

闭包的使用场景：
- 函数作为返回值
- 函数作为参数传递

### 6、异步/同步

前端使用异步的场景：
- 定时任务：setTimeout、setInterval
- 网络请求：ajax,动态<img> ,<script>等
- 事件绑定

> 同步和异步的区别

- 同步会阻塞代码，异步不会
- alert是同步，setTimeout是异步

### 7、DOM节点的attribute和property的区别

DOM （document object model）文档对象模型

- property是对一个js对象的属性的修改。
- attribute是对html标签属性的修改。

### 8、BOM

BOM （browser object model）浏览器对象模型

常用知识点：
- 检测浏览器类型（navigator）
- 解析url各部分（location）
- screen
- history

### 9、AMD和CommonJS

使用场景：
- 需要异步加载JS，使用AMD
- 使用了npm之后建议使用CommonJS，因为npm本身就支持CommonJS。

### 10、上线、回滚流程要点

#### 上线流程：
- 将当前分支的代码提交到git版本库，如果其他已上线分支的代码为合并过来的话，将无法提测，需要先将分支进行合并。
- 将当前服务器的代码全部打包并记录版本号，备份。
- 将需要上线的分支代码提交覆盖到线上服务器，生成新的版本号。

#### 回滚流程
- 将当前服务器的代码打包并记录版本号，备份；
- 将备份的上一个版本号解压，覆盖到线上服务器，并生成新的版本号。

### 11、性能优化

#### 加载资源优化
- 静态资源的压缩合并
- 静态资源缓存
- 使用CDN让资源加载更快
- 使用SSR（服务端渲染）后端渲染，数据直接输出到HTML中。

#### 渲染优化
- CSS放在前面，JS放在页面底部
- 懒加载（图片需要的时候才加载）
- 减少DOM查询，对DOM查询做缓存
- 减少DOM操作，多个操作尽量合并在一起执行
- 事件节流
- 尽早执行操作（DOMContentLoad）
