# <center><font>Taro</font></center>

##一、介绍`Taro`

###1.1简介
`Taro`是一套遵循 `React` 语法规范的 **多端开发** 解决方案
使用`Taro`,可以只书写一套代码，再通过`Taro`的编译工具，将源码分别编译出可以再不同端（微信/百度/支付宝/字节跳动/QQ小程序、快应用、`H5`、`移动端(React-Native)`等）运行的代码。

###1.2特性
1. `React`语法风格：
`Taro`遵循`React`语法规范，它采用与`React`一致的组件化思想，组件生命周期与`React`保持一致，同时支持使用`JSX`语法，使用`Taro`进行开发可以获得和`React`一致的开发体验

代码示例：
```
import Taro, { Component } from '@tarojs/taro'
import { View, Button } from '@tarojs/components'

export default class Index extends Component {
  constructor () {
    super(...arguments)
    this.state = {
      title: '首页',
      list: [1, 2, 3]
    }
  }

  componentWillMount () {}

  componentDidMount () {}

  componentWillUpdate (nextProps, nextState) {}

  componentDidUpdate (prevProps, prevState) {}

  shouldComponentUpdate (nextProps, nextState) {
    return true
  }

  add = (e) => {
    // dosth
  }

  render () {
    return (
      <View className='index'>
        <View className='title'>{this.state.title}</View>
        <View className='content'>
          {this.state.list.map(item => {
            return (
              <View className='item'>{item}</View>
            )
          })}
          <Button className='add' onClick={this.add}>添加</Button>
        </View>
      </View>
    )
  }
}
```

##二、微信小程序转`Taro`
`Taro`可以将你的原生微信小程序应用转换为`Taro`代码，所以可以通过`taro build`的命令将`Taro`代码转换为对应的代码，或者对转换后的`Taro`代码用`React`的方式进行二次开发。

微信原生小程序转`Taro`操作方法：
1. 使用`npm i -g @tarojs/cli`命令安装`Taro`命令行工具
2. 在小程序项目的根目录招工运行：`$ taro convert`
转换后的代码保存在根目录下的`taroConvert`文件夹下。
需要定位到`taroConvert`目录执行`npm install`命令之后就可以使用`taro build`命令编译到对应平台的代码。

**生命周期：**
`Taro`会将原始文件的生命周期钩子函数转换为`Taro`的生命周期，完整对应关系如下：

| Page.onLoad        | componentWillMount   |
-|-|-
| `onShow`      | `componentDidShow`   |
| `onHide`      | `componentDidHide`   |
| `onReady`      | `componentDidMount`   |
| `onUnload`      | `componentWillUnmount`   |
| `onError`      | `componentDidCatchError`   |
| `App.onLaunch`      | `componentWillMount`   |
| `Component.created`      | `componentWillMount`   |
| `attached`      | `componentDidMount`   |
| `ready`      | `componentDidMount`   |
| `detached`      | `componentWillUnmount`   |
| `moved`      | `保留`   |

##三、各端差异
###3.1`React Native`
>如果要支持`React Native`端，必须采用`Flex`布局，并且样式选择器仅支持类选择器，且不支持组合器

以下选择器的写法都是不支持的，在样式转换时会自动忽略。
```
.button.button_theme_islands{
  font-style: bold;
}

img + p {
  font-style: bold;
}

p ~ span {
  color: red;
}

div > span {
  background-color: DodgerBlue;
}

div span { background-color: DodgerBlue; }
```
样式上H5最为灵活，小程序次之，RN最弱；统一多端样式即是对其短板，也就是要以RN的约束来管理样式，同时兼顾小程序的限制，核心可以概括为三点：
* 使用`Flex`布局
* 基于`BEM`写样式
* 采用`style`属性覆盖组件样式
>BEM:块（block）,元素（element）,修饰符（modifier）

RN中`View`标签默认主轴方向时`column`，如果不将其他端改成与RN一直，就需要在所有用到`display:flex`的地方都显式声明主轴方向。

###3.2常见问题

**是否支持全局样式？**
入口文件`app.js`里面引入的样式就是全局样式，本地样式会覆盖全局样式。

**`box-shadow`(添加阴影)能实现吗？**
RN这方面支持得不好（仅ios支持，且支持程度有限）

**RN不支持`backage-image`，有解决办法吗？**
使用`Image`组件

**可以使用微信/支付宝支付吗？**
V1.2.22已支持引入原生的SDK，可以通过跨平台代码实现。

###3.3其他注意事项
* 文字要包在`Text`组件里面，否则不显示
* `position:fixed`RN不支持
* `Animation`和`transform`RN动画不支持
* RN与H5/小程序的`Flex`布局相关属性的默认值有差异

##四、安装使用




