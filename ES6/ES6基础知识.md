# ES6基础知识

### 1、let、const与var的区别

- var声明的变量会有变量提升的特性，将变量的作用域提升到作用域顶部。
- let/const属于块级作用域。
- 使用let声明的变量可以重新赋值，但是不可以在同一作用域内重新声明。
- 使用const声明的变量必须赋值初始化，但是不能在同一作用域内重新声明页无法重新赋值。

### 2、for...of循环

> for循环最大的缺点：需要跟踪计数器和退出条件。

> for...in循环依然需要使用index来访问数组

for...in循环会循环访问所有可枚举的属性，所以如果向数组的原型中添加任何其他属性，这些属性都会出现在循环中。

```
let arr = [12,34,'test',{dig: {a: 123,b:345}}];
for(const index in arr) console.log(arr[index])
```

> for...of循环用于循环访问任何可迭代的数据类型。可以忽略索引。

for...of循环解决了for循环和for...in循环的不足之处，而且可以随时停止或退出for...of循环。

for...of循环只访问循环访问对象中的值。

```
let arr = [12,34,'test',{dig: {a: 123,b:345}}];
for(const item of arr) console.log(item)
```
### 3、Symbol

一种新的基础数据类型，`let s1 = Symbol();`

> 每个Symbol实例都是唯一的，因此比较两个Symbol实例的时候总会返回false。注册相同的全局Symbol时，两个Symbol可以相等。

> Symbol.keyFor() 返回一个已登记的 Symbol 类型值的 key ，用来检测该字符串参数作为名称的 Symbol 值是否已被登记。

```
let a1 = Symbol.for('global_a_1');//注册全局Symbol
let a2 = Symbol.for('global_a_1');//获取全局Symbol

a1 === a2 //true
```
应用场景：
- 使用Symbol来作为对象属性名（key）
- 使用Symbol来代替常量
- 使用Symbol定义类的私有属性方法

> Symbol 值作为属性名时，该属性是公有属性不是私有属性，可以在类的外部访问。但是不会出现在 for...in 、 for...of 的循环中，也不会被 Object.keys() 、 Object.getOwnPropertyNames() 返回。

> 如果要读取到一个对象的Symbol 属性，可以通过 Object.getOwnPropertySymbols() 和 Reflect.ownKeys() 取到。

```
let obj = {
   [Symbol('name')]: '一斤代码',
   age: 18,
   title: 'Engineer'
}

Object.keys(obj)   // ['age', 'title']

for (let p in obj) {
   console.log(p)   // 分别会输出：'age' 和 'title'
}

Object.getOwnPropertyNames(obj)   // ['age', 'title']

JSON.stringify(obj)  // {"age":18,"title":"Engineer"}
```
### 4、展开运算符...

可以将字面量对象展开为多个。

```
const list = ['take bus', 123, 'de'];

console.log(...list);
//take bus 123 de
```
展开运算符可以结合多个数组。作用相当于concat()方法。

```
const food = ['apples','bananas'];
const vege = ['corn','carrots'];
const newfood = [...food,...vege];
console.log(newfood);
//["apples", "bananas", "corn", "carrots"]
```
### 5、Map和Set

#### Map

Map对象保存键值对，任何值（包括对象或原始值）都可以作为一个键或值。

#### Maps与Objects的区别：

- 一个object的键只能是字符串或者Symbol，但是Map可以是任意值。
- Map中的键值是有序的（FIFO原则），添加在object中的键则不是。
- Map键值对的个数可以通过size属性获取，而object只能手动计算。

#### Set

Set对象允许你存储任何类型的唯一值，无论是原始值还是对象引用。

Set中特殊值判断：
- +0与-0在存储判断唯一性是恒等的，所以不重复；
- undefined与undefined是恒等的，所以不重复；
- NaN与NaN不恒等，但是Set中只能存一个，不重复。

> 应用：数组去重

```
let mySet = new Set([1,2,3,3,4,4]);
console.log([...mySet]);//[1,2,3,4]
```
> 并集

```
let arr1 = new Set([1,2,3]);
let arr2 = new Set([2,3,4,5]);
var unionArr = new Set([...arr1, ...arr2]);
```

> 交集

```
let a = new Set([1,2,3]);
let b = new Set([2,3,4]);
let commonArr = new Set([...a].filter(x => b.has(x)));
```

> 差集

```
let a = new Set([1,2,3]);
let b = new Set([2,3,4]);
let diff = new Set([...a].filter(x => !b.has(x)));
```
### 6、弱引用集合WeakSet和WeakMap

Map和Set都为内部的每个键或值保持了强引用，绕过一个对象被删除，回收机制无法取回它占用的内存，除非在Map或者Set中删除它。

WeakSet并不对其中的对象保存强引用，当WeakSet中的一个对象被回收时，它会从WeakSet中移除。WeakMap也一样。因为键是弱引用，在键对象消失后自动释放内存，可以解决内存泄漏问题。

弱引用集合的限制：
- WeakMap只支持new\has\get\set\delete
- WeakSet只支持new\has\add\delete
- WeakSet和WeakMap的键必须是对象
- 都不遍历，所以没有size属性。
- key为弱引用，意味着key引向的对象存在被垃圾回收的可能。

### 7、箭头函数

作用：更简单的函数并且不绑定this。

> [什么时候不可以使用箭头函数](https://www.jianshu.com/p/1357112985ef)

- 定义字面量方法
- 定义原型方法
- 定义事件回调函数
- 定义构造函数

### 8、ES6字符串

- includes():返回布尔值，判断是否找到参数字符串；
- startsWith():返回布尔值，判断参数字符串是否在原字符串的尾部；
- endsWith():返回布尔值，判断参数字符串是否在原字符串的尾部。
- repeat():返回新的字符串，表示将字符串重复指定次数返回。
- padStart():返回新的字符串，表示用参数字符串从头部补全原字符串。
- padEnd():返回新的字符串，表示用参数字符串从尾部补全原字符串。

### 9、ES6模块export与import

特点：
- 导出的函数声明与类声明必须要有名称（export default命令除外）；
- 不仅能导出声明还能导出引用（如函数）；
- export命令可以出现在模块的任何位置，但必须处于模块顶层；
- import命令会提升到整个模块的头部，首先执行。
- export命令导出的接口名称，必须和模块内部的变量有一一对应关系。
- import命令不允许在加载的脚本里面改写接口的引用指向，即可以改写import变量类型的对象的属性值，不能改写import变量类型为基本类型的值。

> export default命令特点：

- 在一个文件或模块中，export、import可以有多个，但是export default仅有一个；
- export default中的default是对应的导出接口变量；
- 通过export方式导出，在导入时要加{}，export default 则不需要；
- export default 向外暴露的成员，可以使用任意变量来接收。
