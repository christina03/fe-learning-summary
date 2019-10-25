# TypeScript基础语法解析

### 1、字符串新特性

##### （1）多行字符串

```
var str = `aaa
bbb
ccc`;
```
##### （2）字符串模板

```
var name = "zhang san";
var getName = function(){
    return "zhang san";
}

console.log(`hello ${name}`);
console.log(`hello ${getName()}`);
console.log(`<div>
<span>${name}</span>
</div>`)
```
##### （3）自动拆分字符串

```
function test(tpl, name, age){
    console.log(tpl);
    console.log(name);
    console.log(age);
}

var name = "zhang san";
var getAge = function(){
    return 18;
}

test`hello my name is ${name}, I'am ${getAge()}`
```
### 2、参数新特性

##### （1）参数类型

在参数名称后面使用冒号来指定参数的类型。

```
var name: string = "zhang san";
var a1: any = "aaa"; // any类型表示可以是任意类型的值
var a2: number = 2;
var a3: boolean = true;
function test(name: string): void{
    // void类型表示该方法不需要返回值，如果有返回值则会报错
}

// 自定义类型
class Person {
    name: string,
    age: number
}
var zhangsan: Person = new Person();
zhangsan.name = "zhang san";
zhangsan.age = 18;
```
##### （2）默认参数

在参数声明后面用等号来指定参数的默认值。

```
// 给方法参数指定默认值
function test(a: string, b: string, c: number = 20){
    console.log(a);
    console.log(b);
    console.log(c);
}
```
##### （3）可选参数

在方法的参数声明后面用问号来标明次参数为可选参数。

```
// 给b参数加?表示可选，此时需要在函数体里兼容处理没传b参数的相关代码
function test(a: string, b?: string, c: number = 20){
    console.log(a);
    console.log(b);
    console.log(c);
}
```
### 3、函数新特性

##### （1）Rest and Spread操作符

用来声明任意数量的方法参数。

```
// 表示可以传任意数量的参数
function func(...args) {
    args.forEach(function(arg)){
        console.log(arg);
    }
}

// 参数数量固定，调用的时候做处理
function func2(a, b, c){
    console.log(a);
    console.log(a);
    console.log(a);
}

var arr1 = [1,2];
var arr2 = [7,8,9,10,11];
func2(...arr1);// 打印出1 2 undefinded
func2(...arr2);//打印出7 8 9
```
##### （2）generator函数

控制函数的执行过程，手工暂停和恢复代码执行。

```
// 在function后面加个*号就是generator函数了
function* doSomething(){
    console.log("start");
    
    yield; // 相对于打了个断点
    
    console.log("end");
}

var func = doSomething(); // 需要声明一个变量才能执行

func.next() // start
func.next() // end

```
##### （3）destructuring析构表达式

通过表达式将对象或数组拆解成任意数量的变量。

```
function getStock(){
    return {
        code: "IWD",
        price: 80
    }
}
var {code, price} = getStock(); // 声明两个变量，并对其赋值（变量名要与方法里面的名称一样）

// 设置别名
var {code: code2, price} = getStock();

// 获取嵌套的变量
function getStock2(){
    return {
        code: "ikl",
        price: {
            price1: 100,
            price2: 200
        }
    }
}

var {code, price: {price2}} = getStock2();
console.log(code); // ikl
console.log(price2); // 200

// 数组的析构表达式
var arr1 = [1,2,3,4];
var [num1, , , num2] = arr1;
console.log(num1); // 1
console.log(num2); // 4

var [num3, num4, ...others] = arr1;
console.log(others); // 打印出3和4组成的数组

// 析构表达式作为函数参数
function doSomething([num1, num2, ...others]){
    console.log(num1); // 1
    console.log(num2);// 2
    console.log(others);// [3,4]
}
```
### 4、表达式和循环

##### （1）箭头表达式

用来声明匿名函数，消除传统匿名函数的this指针问题。

```
// 最简单的匿名函数
var sum = (arg1, arg2) => arg1 + arg2;
```

##### （2）forEach(),for in和for of

```
var myArr = [1,2,3,4];
mayArr.desc = "four number"; // 这么赋值在TypeScript是不可以这么写的，这里仅仅为了测试
// forEach只能循环打印出1,2,3,4;而且不可以break

// for in
for(var n in myArr){
    console.log(myArr[n]); // 1,2,3,4,"four number" （打印出值）
    console.log(n); // 1,2,3,4,desc (打印出的是键)
}

// for of 循环可以被打断,循环的也是数组或对象的值，并不包括属性值

for(var m in myArr){
    if(m > 2) break;
    console.log(m); // 1,2
}
```
### 5、面向对象特性