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

##### （1）类（Class）

类是TypeScript的核心，使用TypeScript开发时，大部分代码都是写在类里面的。

###### 类的定义

```
// 访问控制符public/private/protected，不加的时候默认是public
class Person {
    private name; // 此时无法在外部访问到
    eat(){
        console.log('I'm eating');
    }
}

// 类的实例化
var p1 = new Person();
```
###### 构造函数

```
class person2{
    // 构造函数不能在外部进行访问，它只在实例化的时候执行一次
    // 在构造函数上声明访问控制符，这么写的时候表示声明了一个name属性，并且实例化的时候要为其赋值
    constructor(public name: string){ 
        
    }
    eat(){
        console.log(this.name);
    }
}

var p = new Person('zhangsan'); // 输出zhangsan
```

###### 类的继承

```
class person2{
    constructor(public name: string){ 
        console.log('haha');
    }
    eat(){
        console.log(this.name);
    }
}

class Employee extends Person{
    constructor(name: string, code: string){
        super(name); // 子类构造函数必须要调用父类构造函数，通过super()方法调动
        this.code = code;
        console.log('xixi');
    }
    work(){
        super.eat();// 通过super调用父类方法
        this.doWork();
    }
    private doWork(){
        console.log('do work')
    }
}

var p1 = new Employee('ceshi'); // ceshi
```
##### （2）泛型（generic）

参数化的类型，一般用来限制集合的内容。

```
class person2{
    constructor(public name: string){ 
        console.log('haha');
    }
    eat(){
        console.log(this.name);
    }
}

var workers: Array<Person> = [];
workers[0] = new Person("ceshi");
```
##### （3）接口（Interface）

用来建立某种代码约定，使得其它开发者在调用某个方法或创建新的类时必须遵循接口所定义的代码约定。

```
// 实例一：接口作为函数参数
interface IPerson{
    name: string;
    age: number;
}

class Person{
    constructor(public config: IPerson){
        
    }
}

var p1 = new Person({
    name: "zhangsan",
    age: 18
})
```

```
// 实例二：声明实现接口的类里面必须实现接口里面的方法
interface Animal{
    eat();
}

class Sheep implements Animal{
    eat(){ // 该方法必须写
        console.log('eat grass');
    }
}
```
##### （4）模块（Module）

模块可以帮助开发者将代码分割为可重用的单元。开发者可以自己决定将模块中的哪些资源（类、方法、变量）暴露出去供外部使用，哪些资源只在模块内使用。

##### （5）注解（annotation）

注解为程序的元素（类、方法、变量）加上更直观明了的说明，这些说明信息与程序的业务逻辑无关，而是供指定的工具或框架使用的。

##### （6）类型定义文件（*.d.ts）

类型定义文件用来帮助开发者在TypeScript中使用已有的JavaScript的工具包，如：JQuery。

一些基本的类型定义文件：
[DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)
