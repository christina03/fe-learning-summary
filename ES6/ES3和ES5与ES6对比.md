# ES3和ES5与ES6对比

### 1、块作用域

在es6中用一对`{}`就可以实现块作用域。

### 2、默认参数、可变参数计算、数组拼接

ES3\ES5默认参数的写法
```
{
    //es5/es3默认参数
    function f(x,y,z){
        if(y === undefinded){
            y = 7;
        }
        if(z === undefinded){
            z = 42;
        }
        return x+y+z;
    }
    console.log(f(1,3));
}
```
ES6默认参数的写法

```
{
    //ES6默认参数
    function f(x, y = 7, z=42){
        return x+y+z;
    }
    console.log(f(1,3));
}
```
ES3,ES5可变参数获取：

```
{
    //ES3,ES5可变参数获取
    function f(){
        var a = Array.prototype.slice.call(arguments);
        var sum = 0;
        a.forEach(function(item){
            sum += item*1;
        });
        return sum
    }
    console.log(f(1,2,3,4));
}
```
ES6可变参数写法：

```
{
    function f(...a){
        var sum = 0;
        a.forEach((item)=>{
            sum += item*1
        })
        return sum;
    }
    console.log(f(1,3,4,6));
}
```
ES5数组合并：

```
{
    //es5 数组合并
    var params = [1, 'hi', true];
    var other = [2,3].concat(params);
}
```
ES6数组合并

```
{
    //es6 数组合并
    var params = [1, 'hi', true];
    var other = [2,3, ...params];
}
```



### 3、对象代理

> 定义不可修改的对象：

下面是ES3实现方法：
```
//es3中
{
    var Person = function(){
        var data = {
            name: 'es3',
            sex: 'male',
            age: 15
        }
        this.get = function(key){
            return data[key];
        }
        this.set = function(key, value){
            if(key !== 'sex'){
                data[key] = value;
            }
        }
    }
    //声明一个实例
    var person = new Person();
    console.table({
        name: person.get('name'),
        sex: person.get('sex'),
        age: person.get('age')
    })
}
```
下面是es5实现方法：

```
{
    //ES5
    var Person = {
        name: 'es5',
        age: 16
    };
    Object.defineProperty(Person, 'sex',{
        writable: false,
        value: 'male'
    })
}
```
下面是ES6的实现方式：

```
{
    //es6
    let Person = {
        name: 'es6',
        sex: 'male',
        age: 17
    };
    let person = new Proxy(Person, {
        get(target, key){
            return target[key]
        },
        set(target, key, value){
            if(key !== 'sex'){
                target[key] = value;
            }
        }
    });
    
    console.table({
        name: person.name,
        sex: person.sex,
        age: person.age
    });
    //person.sex = 'female';此时会报错
}
```

