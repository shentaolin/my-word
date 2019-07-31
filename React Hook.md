# <center><font color='red'>React Hook</font></center>

> Hook是React 16.8 的新增特性。它可以让你在不编写class的情况下使用state以及其他的React特性。

##一、Hook动机
**1. 在组件之间复用状态逻辑困难**
Hook 使你在无需修改组件结构的情况下复用状态逻辑。 这使得在组件间或社区内共享 Hook 变得更便捷。

**2. 复杂组件变得难以理解**
Hook 将组件中相互关联的部分拆分成更小的函数，而并非强制按照生命周期划分。

**3. 难以理解的class**
Hook 使你在非 class 的情况下可以使用更多的 React 特性。



##二、Hook 体验


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

`useState`就是一个`Hook`，可以在我们不使用`class`组件的情况下，拥有自身的`state`，并且可以通过修改`state`来控制UI的展示。

---

##三、常用的两个Hook


###1. useState
>返回一个state，以及更新state的函数

**语法**

> const [state,setState] = useState(initialState)

* 传入唯一的参数：`initialState`，可以是数字，字符串等，也可以是对象或者数组。
    ```
    const [age, setAge] = useState(42);
    const [fruit, setFruit] = useState('banana');
    const [todos, setTodos] = useState([{ text: '学习 Hook' }]);
    ```

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


###2. useEffect
之前很多具有副作用的操作，例如网络请求，修改UI等，一般都是在`class`组件的`componentDidMount`或者`componentDidUpdate`等生命周期中进行操作。而在函数组件中是没有这些生命周期的概念的，只能`return`想要渲染的元素。但是现在，在函数组件中也有执行副作用操作的地方了，就是使用`useEffect`函数。

**语法**
> useEffect(() => { doSomething });

两个参数：
* 第一个是一个函数，是在第一次渲染以及之后更新渲染之后会进行的副作用。
    * 这个函数可能会有返回值，倘若有返回值，返回值也必须是一个函数，会在组件被销毁时执行。

* 第二个参数是可选的，是一个数组，数组中存放的是第一个函数中使用的某些副作用属性。用来优化useEffect
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
> 不仅如此，我们可以使一公共useEffect执行多个副作用（可以使用一个useEffect执行多个副作用，也可以分开执行）
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
**清除effect**
> 我们一般会在`componentWillUnmount`声明周期中进行移除注册的事件等操作。那么在函数组件中该如何操作呢？
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
        window.unaddEventListener('click', handleClick);
    }
});
```
可以看到，我们传入的第一个参数，可以return一个函数出去，**在组件被销毁时，会自动执行这个函数。**

**优化useEffect**
上面我们使用的都是`useEffect`中的第一个参数，传入了一个函数。那么`useEffect`的第二个参数呢？

`useEffect`的第二个参数是一个数组，里面放入在useEffect使用到的state值，可以用作优化，只有当数组中state值发生变化时，才会执行这个`useEffect`。

```
useEffect(() => {
    // 使用浏览器API更新文档标题
    document.title = `You clicked ${count} times`;
}, [ count ]);// 仅在 count 更改时更新
```
> 如果想模拟class组件的行为，只在componentDidMount时执行副作用，在componentDidUpdate时不执行，那么`useEffect`的第二个参数传一个空数组[]即可。


---
##四、Hook顺序
>可以在单个组件中使用多个 State Hook 或 Effect Hook
```
function Form() {
  // 1. Use the name state variable
  const [name, setName] = useState('Mary');

  // 2. Use an effect for persisting the form
  useEffect(function persistForm() {
    localStorage.setItem('formData', name);
  });

  // 3. Use the surname state variable
  const [surname, setSurname] = useState('Poppins');

  // 4. Use an effect for updating the title
  useEffect(function updateTitle() {
    document.title = name + ' ' + surname;
  });

  // ...
}
```
React怎么知道哪个state对应哪个`useState`？答案是靠的是Hook调用的顺序。
```
// ------------
// 首次渲染
// ------------
useState('Mary')           // 1. 使用 'Mary' 初始化变量名为 name 的 state
useEffect(persistForm)     // 2. 添加 effect 以保存 form 操作
useState('Poppins')        // 3. 使用 'Poppins' 初始化变量名为 surname 的 state
useEffect(updateTitle)     // 4. 添加 effect 以更新标题

// -------------
// 二次渲染
// -------------
useState('Mary')           // 1. 读取变量名为 name 的 state（参数被忽略）
useEffect(persistForm)     // 2. 替换保存 form 的 effect
useState('Poppins')        // 3. 读取变量名为 surname 的 state（参数被忽略）
useEffect(updateTitle)     // 4. 替换更新标题的 effect

// ...
```

只要Hook的调用顺序在多次渲染之间保持一致，React就能正确的将内部state和对应的Hook进行关联

---
##五、Hook规则
>Hook本质就是JavaScript函数，但是在使用它时需要遵循两条规则。

1. **只在最顶层使用Hook**

**不要在循环、条件或嵌套函数中调用Hook，确保总是在React函数的最顶层调用它们。** 遵守这条规则就能确保Hook在每一次渲染中都按照同样的顺序被调用。这让React能够在多次的`useState`和`useEffect`调用之间保持hook状态的正确。

**如果想要有条件的执行一个effect，可以将判断放在Hook内部**
```
useEffect(function persistForm() {
    // 将条件判断放置在 effect 中
    if (name !== '') {
        localStorage.setItem('formData', name);
    }
});
```

2. **只在React函数中调用Hook**

**不要在普通JavaScript函数中调用Hook。** 可以：
* 在React的函数组件中调用Hook
* 在自定义Hook中调用其他Hook

---
##六、自定义Hook
>自定义Hook是一个函数，其名称以`use`开头，函数内部可以调用其他的Hook。

如下面的`useFriendStatus`是第一个自定义的Hook：
```
import React, { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```
与组件中一致，确保只在自定义Hook的顶层无条件的调用其他Hook。

此处`useFriendStatus`的Hook目的是订阅某个好友的在线状态。这就是需要将`friendID`作为参数，并返回这位好友的在线状态的原因。

```
function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  // ...

  return isOnline;
}
```
**如何使用自定义Hook**
>目标是在`FriendStatus`和`FriendListItem`组件中去除重复的逻辑，即：这两个组件都想知道好友是否在线。

```
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);//自定义组件使用

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```
```
function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);//自定义组件使用

  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```

**总结：**
* **自定义Hook必须以`use`开头；** 这个约定非常重要。不遵循的话，由于无法判断某个函数是否包含对其内部Hook的调用，React将无法自动检查你的Hook是否违反了Hook的规则。

* **在两个组建中使用相同的Hook不会共享state；** 自定义Hook是一种重用状态逻辑的机制（例如设置为订阅并存储当前值），所以每次使用自定义Hook时，其中的所有state和副作用都是完全隔离的。

* **每次调用Hook，它都会获取独立的state；** 

