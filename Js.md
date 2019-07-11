# <center>Js</center>

##async/await
>用 async/await 来处理异步; (async就是异步的意思)

**<font color=red size=4>异步函数也就意味着该函数的执行不会阻塞后面代码的执行</font>**

```
<!-- 代码示例： -->
async function timeout() {
    return 'hello world'
}
timeout().then(result => {
    console.log(result);
})
console.log('虽然在后面，但是我先执行');

<!-- 输出结果： -->
虽然在后面，但是我先执行
hello world
```

##`join()`数组转字符串
>需要将数组元素用某个字符连接成字符串
```
var a, b;
a = new Array(0,1,2,3,4);
b = a.join("-");      //"0-1-2-3-4"
```

##`split()`字符串转数组
>将字符串按某个字符切割成若干个字符串，并以数组形式返回
```
var s = "abc,abcd,aaa";
ss = s.split(",");// 在每个逗号(,)处进行分解  ["abc", "abcd", "aaa"]
var s1 = "helloworld";
ss1 = s1.split('');  //["h", "e", "l", "l", "o", "w", "o", "r", "l", "d"]
```

##`splice()`数组添加/删除项目
>该方法会改变原始数组
```
var s=['a','b','c'];
console.log(s.splice(2,1)); // 打印["c"]
console.log(s); // 打印["a", "b"]
```

##`substring()`
>返回一个索引和另一个索引之间的字符串
`str.substring(indexStart, [indexEnd])`
```
var str = 'abcdefghij';
str.substring(1, 2));   // b
```

##`substr()`
>返回从指定位置开始的字符串中指定字符数的字符
`str.substr(start, [length])`
```
var str = 'abcdefghij';
str.substr(1, 2));   // bc
```

##`trim()`
>去掉字符序列左边和右边的空格;
字符串中间的空格不进行处理
```
str = " i love you    "
str = trim(str);    //i love you
```
