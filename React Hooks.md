# React Hooks

> 16.8 版本之后 React 发布的新特性 Hooks 

## Hooks简介
---

`Hooks` 是 `React v16.7.0-alpha` 中加入的新特性。

你还在为该使用无状态组件（Function）还是有状态组件（Class）而烦恼吗？
——拥有了hooks，你再也不需要写Class了，你的所有组件都将是Function。

你还在为搞不清使用哪个生命周期钩子函数而日夜难眠吗？
——拥有了Hooks，生命周期钩子函数可以先丢一边了。

你在还在为组件中的this指向而晕头转向吗？
——既然Class都丢掉了，哪里还有this？你的人生第一次不再需要面对this。

---

## Hooks 初体验
---

Example.js

```
import React, { useState  } from 'react';

function Example() {
    // 声明一个名为“count”的新状态变量
    const [count, setCount] = useState(0);

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
                Click me
            </button>
        </div>
    );
}

export default Example;
```

`useState`就是一个`Hook`，可以在我们不适用`class`组件的情况下，拥有自身的`state`，并且可以通过修改`state`来控制UI的展示。

---

## 常用的两个Hooks
---

####1. useState

**语法**

> const [state,setState] = useState(initialState)

* 传入唯一的参数：`initialState`，可以是数字，字符串等，也可以是对象或者数组。

* 返回的是包含两个元素的数组：第一个元素，`state`变量，`setState`修改state值得方法。

**与在类中使用`setState`的异同点：**

* 相同点：也是异步的，例如在`onClick`事件中，调用两次`setState`，数据只改变一比。

* 不同点：类中的`setState`是合并，而函数组件中的`setState`是替换。

**使用对比**

之前想要使用组件内部的状态，必须使用class组件，例如：

Example.js

```
import React, { Component } from 'react';

export default class Example extends Component {
    constructor(props) {
        super(props);
        this.state = {
            count: 0
        };
    }

    render() {
        return (
            <div>
            <p>You clicked {this.state.count} times</p>
            <button onClick={() => this.setState({ count: this.state.count + 1 })}>
                Click me
            </button>
            </div>
        );
    }
}
```

而现在，我们使用函数式组件也可以实现一样的功能了。也就意味着函数式组件内部也可以使用state了。

Example.js
```
import React, { useState } from 'react';

function Example() {
    // 声明一个名为“count”的新状态变量
    const [count, setCount] = useState(0);

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
                Click me
            </button>
        </div>
    );
}

export default Example;
```

**优化**

创建初始状态是比较昂贵的，所以我们可以在使用`useState`API时，传入一个函数，就可以避免重新创建忽略的初始状态。

普通的方式：
```
// 直接传入一个值，在每次 render 时都会执行 createRows 函数获取返回值
const [rows, setRows] = useState(createRows(props.count));
```

优化后的方式：
```
// createRows 只会被执行一次
const [rows, setRows] = useState(() => createRows(props.count));
```

####2. useEffect
之前很多具有副作用的操作，例如网络请求，修改UI等，一般都是在`class`组件的`componentDidMount`或者`componentDidUpdate`等生命周期中进行操作。而在函数组件中是没有这些生命周期的概念的，只能`return`想要渲染的元素。但是现在，在函数组件中也有执行副作用操作的地方了，就是使用`useEffect`函数。

**语法**
> useEffect(() => { doSomething });

两个参数：
* 第一个是一个函数，是在第一次渲染以及之后更新渲染之后会进行的副作用。
    * 这个函数可能会有返回值，倘若有返回值，返回值也必须是一个函数，会在组件被销毁时执行。

* 第二个蚕食是可选的，是一个数组，数组中存放的是第一个函数中使用的某些副作用属性。用来优化useEffect
    * 如果使用此优化，请确保该数组包含外部作用域中随时间变化且effect使用的任何值。否则，你的代码将引用先前渲染中的旧值。
    * 如果要运行effect并仅将其清理一次（在装载和卸载时）,则可以将空数组（[]）作为第二个参数传递。这告诉react你的effect不依赖于来自props或state的任何值，所以它永远不需要重新运行。

> 虽然传递[]更接近熟悉的`conponentDidMount`和`componentWillUnmount`执行规则，但建议不要将它作为一种习惯，因为它经常会导致错误。

**使用对比**
假如此时有一个需求，让document的title与Example中的count次数保持一致。
使用class组件：
Example.js
```
import React, { Component } from 'react';

export default class Example extends Component {
    constructor(props) {
        super(props);
        this.state = {
            count: 0
        };
    }

    componentDidMount() {
        document.title = `You clicked ${ this.state.count } times`;
    }

    componentDidUpdate() {
        document.title = `You clicked ${ this.state.count } times`;
    }

    render() {
        return (
            <div>
            <p>You clicked {this.state.count} times</p>
            <button onClick={() => this.setState({ count: this.state.count + 1 })}>
                Click me
            </button>
            </div>
        );
    }
}
```
而现在在函数组件中也可以进行副作用操作了。
Example.js
```
import React, { useState, useEffect } from 'react';

function Example() {
    // 声明一个名为“count”的新状态变量
    const [count, setCount] = useState(0);

    // 类似于 componentDidMount 和 componentDidUpdate:
    useEffect(() => {
        // 使用浏览器API更新文档标题
        document.title = `You clicked ${count} times`;
    });

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
                Click me
            </button>
        </div>
    );
}

export default Example;
```
> 不仅如此，我们可以施一公useEffect执行多个副作用（可以使用一个useEffect执行多个副作用，也可以分开执行）
```
useEffect(() => {
    // 使用浏览器API更新文档标题
    document.title = `You clicked ${count} times`;
});

const handleClick = () => {
    console.log('鼠标点击');
}

useEffect(() => {
    // 给 window 绑定点击事件
    window.addEventListener('click', handleClick);
});
```
> 现在看来功能差不多了。但是在使用类组件时，我们一般会在`componentWillMount`声明周期中进行移除注册的事件等操作。那么在函数组件中该如何操作呢？
```
useEffect(() => {
    // 使用浏览器API更新文档标题
    document.title = `You clicked ${count} times`;
});

const handleClick = () => {
    console.log('鼠标点击');
}

useEffect(() => {
    // 给 window 绑定点击事件
    window.addEventListener('click', handleClick);

    return () => {
        // 给 window 移除点击事件
        window.addEventListener('click', handleClick);
    }
});
```
可以看到，我们传入的第一个参数，可以return一个函数出去，**在组件被销毁是，会自动执行这个函数。**

**优化useEffect**
上面我们使用的都是`useEffect`中的第一个参数，传入了一个函数。那么`useEffect`的第二个参数呢？

`useEffect`的第二个参数是一个数组，里面放入在useEffect使用到的state值，可以用作优化，只有当数组中state值发生变化时，才会执行这个`useEffect`。

```
useEffect(() => {
    // 使用浏览器API更新文档标题
    document.title = `You clicked ${count} times`;
}, [ count ]);
```
> 如果想摸你class组件的行为，只在componentDidMount时执行副作用，在componentDidUpdate时不执行，那么`useEffect`的第二个参数传一个[]即可。（不建议这么做，可能会由于疏漏出现错误）
