# <center><font color='red'>Less</font></center>

>## Less特点
>* 导入
>* 变量 - 它可以让你更轻松的在整个样式表中定义和更改值
>* 混合 - 可以让你重用或者组合样式，而且支持传递参数
>* 嵌套
>* 运算 - 动态计算值，`css`中最近出了一个`calc()`,但它只适合用于长度的计算
>* 函数 - 它为你提供了一些方便的程序去操纵颜色，转换图像等
>* 继承


##一、导入

1. 导入less文件可省略后缀
    ```
    import "main"; 
    //等价于
    import "main.less";
    ```

2. `@import`的位置可随意放置
  ```
  #main{
    font-size:15px;
  }
  @import "style";
  ```

###3.once
>`@import`语句的默认行为。这表明相同的文件只会被导入一次，而随后的导入文件的重复代码都不会解析
```
@import (once) "foo.less";
@import (once) "foo.less"; // 此语句将被忽略
```


---
##变量
`Less`的一个主要功能就是可以让你像在其它高级语言中一样声明变量，这样你就可以存储你经常使用的 任何类型的值：颜色，尺寸，选择器，字体名称和`URL`等。`less`就是让你在可能的情况下重用CSS语法

>以 `@` 开头 定义变量，并且使用时 直接 键入 `@` 名称

这里，声明了两个变量，一个是背景颜色，一个是文本颜色，它们都是十六进制的值

`Less`代码如下：
```
/* Less */
@background-color: #ffffff;
@text-color: #1A237E;
p{
  background-color: @background-color;
  color: @text-color;
  padding: 15px;
}
ul{
  background-color: @background-color;
}
li{
  color: @text-color;
}

/* 生成后的 CSS */
p{
    background-color: #ffffff;
    color: #1A237E;
    padding: 15px;
}
ul{
    background-color: #ffffff;
}
li{
    color: #1A237E;
}
```





---
##混合
`Less`允许将已有的`class`和`id`的样式应用到另一个不同的选择器上。例：
```
/* Less */
#circle{
  background-color: #4CAF50;
  border-radius: 100%;
}
#small-circle{
  width: 50px;
  height: 50px;
  #circle
}
#big-circle{
  width: 100px;
  height: 100px;
  #circle
}

/* 生成后的 CSS */
#circle {
    background-color: #4CAF50;
    border-radius: 100%;
}
#small-circle {
    width: 50px;
    height: 50px;
    background-color: #4CAF50;
    border-radius: 100%;
}
#big-circle {
    width: 100px;
    height: 100px;
    background-color: #4CAF50;
    border-radius: 100%;
}
```






如果不想混合也以一种规则的形式出现在`css`代码中，那么可以在它的后面加上括号：
```
/* Less */
#circle(){
    background-color: #4CAF50;
    border-radius: 100%;
}
#small-circle{
    width: 50px;
    height: 50px;
    #circle
}
#big-circle{
    width: 100px;
    height: 100px;
    #circle
}

/* 生成后的 CSS */
#small-circle {
    width: 50px;
    height: 50px;
    background-color: #4CAF50;
    border-radius: 100%;
}
#big-circle {
    width: 100px;
    height: 100px;
    background-color: #4CAF50;
    border-radius: 100%;
}
```





混合另一个比较酷的功能就是它支持传入参数，下面这个例子就为`circle`传入一个指定宽高的参数，默认是25px。这将创建一个25*25的小圆和一个100*100的大圆

```
/* Less */
#circle(@size: 25px){
    background-color: #4CAF50;
    border-radius: 100%;

    width: @size;
    height: @size;
}
#small-circle{
    #circle
}
#big-circle{
    #circle(100px)
}

/* 生成后的 CSS */
#small-circle {
    background-color: #4CAF50;
    border-radius: 100%;
    width: 25px;
    height: 25px;
}
#big-circle {
    background-color: #4CAF50;
    border-radius: 100%;
    width: 100px;
    height: 100px;
}
```





---
##嵌套
嵌套可用以与页面的HTML结构想匹配的方式构造样式表，同时减少了冲突的机会。下面是一个无序列表的例子：
```
/* Less */
ul{
    background-color: #03A9F4;
    padding: 10px;
    list-style: none;

    li{
        background-color: #fff;
        border-radius: 3px;
        margin: 10px 0;
    }
}

/* 生成后的 CSS */
ul {
    background-color: #03A9F4;
    padding: 10px;
    list-style: none;
}
ul li {
    background-color: #fff;
    border-radius: 3px;
    margin: 10px 0;
}
```





就像在其他高级语言中一样，`Less`的变量根据范围接受它们的值。如果在指定范围内没有关于变量值的声明，`less`会一直往上查找，直至找到离它最近的声明。

回到`CSS`中来，`li`标签将有白色的文本，如果在`ul`标签中声明`@text-color`规则：
```
/* Less */
@text-color: #000000;
ul{
    @text-color: #fff;
    background-color: #03A9F4;
    padding: 10px;
    list-style: none;

    li{
        color: @text-color;
        border-radius: 3px;
        margin: 10px 0;
    }
}

/* 生成后的 CSS */
ul {
    background-color: #03A9F4;
    padding: 10px;
    list-style: none;
}
ul li {
    color: #ffffff;
    border-radius: 3px;
    margin: 10px 0;
}
```



###& 的妙用
>& ：代表的上一层选择器的名字，此例便是header
```
/* Less */
#header{
  &:after{
    content:"Less is more!";
  }
  .title{
    font-weight:bold;
  }
  &_content{//理解方式：直接把 & 替换成 #header
    margin:20px;
  }
}

/* 生成后的 CSS */
#header::after{
  content:"Less is more!";
}
#header .title{ //嵌套了
  font-weight:bold;
}
#header_content{//没有嵌套！
    margin:20px;
}
```


---
## 运算

可以对数值和颜色进行基本的数学运算。比如说想要两个紧邻的`div`标签，第二个标签是第一个标签的两倍宽并且拥有不同的背景色

```
/* Less */
@div-width: 100px;
@color: #03A9F4;
div{
    height: 50px;
    display: inline-block;
}
#left{
    width: @div-width;
    background-color: @color - 100;
}
#right{
    width: @div-width * 2;
    background-color: @color;
}

/* 生成后的 CSS */
div {
    height: 50px;
    display: inline-block;
}
#left {
    width: 100px;
    background-color: #004590;
}
#right {
    width: 200px;
    background-color: #03a9f4;
}
```



---
##函数

`Less`中也有函数，这让它看起来像一门编程语言

比如`fadeout`，下面是一个降低颜色透明度的函数：
```
/* Less */
@var: #004590;

div{
  height: 50px;
  width: 50px;
  background-color: @var;

  &:hover{
    background-color: fadeout(@var, 50%)
  }
}

/* 生成后的 CSS */
div {
    height: 50px;
    width: 50px;
    background-color: #004590;
}
div:hover {
    background-color: rgba(0, 69, 144, 0.5);
}
```


---
## 继承
`extend` 是 `Less` 的一个伪类。它可继承所匹配声明中的全部样式。
###1.`extend`关键字的使用
```
/* Less */
.animation{
    transition: all .3s ease-out;
    .hide{
      transform:scale(0);
    }
}
#main{
    &:extend(.animation);
}
#con{
    &:extend(.animation .hide);
}

/* 生成后的 CSS */
.animation,#main{
  transition: all .3s ease-out;
}
.animation .hide , #con{
    transform:scale(0);
}
```

###2.`all`全局搜索替换
使用选择器匹配到的全部声明
```
/* Less */
#main{
  width: 200px;
}
#main {
  &:after {
    content:"Less is good!";
  }
}
#wrap:extend(#main all) {}

/* 生成的 CSS */
#main,#wrap{
  width: 200px;
}
#main:after, #wrap:after {
    content: "Less is good!";
}
```