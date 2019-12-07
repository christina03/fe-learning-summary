# JS实现千分位分割

### 1、采用正则表达式实现

```
function separatorRegNumber(number){
    let result = number.toString().replace(/\d+/, function(n){ // 先提取整数部分
        return n.replace(/(\d)(?=(\d{3})+$)/g,function($1){
            return $1+",";
        });
    });
    return result;
}

```

### 2、采用toLocaleString()实现

```
function separatorNumber(number){
    return number.toLocaleString();
}
```

### 3、采用原始方法实现

```
function separatorOriginalNumber(number){
    let num = number.toString().split('.'); // 分割小数点
    let numArr = num[0].split('').reverse();
    let result = [];
    let res = '';
    numArr.map((item,i) => {
        if(i%3 === 0 && i !== 0){
            result.push(',');
        }
        result.push(item);
        return item;
    });
    result.reverse();
    if(num.length>1 && num[1]){
        res = result.join('') + '.' + num[1];
    } else {
        res = result.join('');
    }
    return res;
}
```
