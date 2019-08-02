# <center><font color='red'>小程序</font></center>

##一、目录结构

小程序包含一个描述整体程序的 `app` 和多个描述各自页面的 `page`。

一个小程序主体部分由三个文件组成，必须放在项目的根目录，如下：

文件|必需|作用
:--|:--|:--
app.js|是|小程序逻辑
app.json|是|小程序公共配置
app.wxss|否|小程序公共样式表

一个小程序页面由四个文件组成，分别是：

文件类型|必需|作用
:--|:--|:--
js|是|页面逻辑
wxml|是|页面结构
json|否|页面配置
wxss|否|页面样式表


##二、配置小程序

###1.全局配置
小程序根目录下的 `app.json` 文件用来对微信小程序进行全局配置

```
{
  <!-- 页面路径列表 -->
  "pages": [
    "pages/index/index",
    "pages/test/test",
    "pages/demo/demo"
  ],
  <!-- 全局的默认窗口表现 -->
  "window": {
    "backgroundTextStyle": "light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "WeChat",
    "navigationBarTextStyle": "black"
  },
  <!-- 底部 tab 栏的表现 -->
  "tabBar": {
    "backgroundColor": "#f5f5f5",
    "color": "#000000",
    "selectedColor": "#eb4e4e",
    "borderStyle": "black",
    "list": [
      {
        "pagePath": "pages/index/index",
        "text": "首页",
        "iconPath": "assets/index.png",
        "selectedIconPath": "assets/index-select.png"
      },
      {
        "pagePath": "pages/test/test",
        "text": "测试",
        "iconPath": "assets/test.png",
        "selectedIconPath": "assets/test-select.png"
      }
    ]
  },
  "sitemapLocation": "sitemap.json"
}
```

###2.页面配置
每一个小程序页面也可以使用同名 `.json` 文件来对本页面的窗口表现进行配置，页面中配置项会覆盖 `app.json` 的 `window` 中相同的配置项。

```
{
  "usingComponents": {},//页面自定义组件配置
  "navigationBarBackgroundColor": "#ffffff",//导航栏背景颜色
  "navigationBarTextStyle": "black",//导航栏标题颜色，仅支持 black / white
  "navigationBarTitleText":"首页",//导航栏标题文字内容	
  "backgroundTextStyle": "light"//下拉 loading 的样式，仅支持 dark / light	
}
```

###3.sitemap 配置
小程序根目录下的 `sitemap.json` 文件用于配置小程序及其页面是否允许被微信索引，文件内容为一个 `JSON` 对象，如果没有 `sitemap.json` ，则默认为所有页面都允许被索引

##三、生命周期

生命周期|触发
:--|:--
`onLoad(){}`|监听页面加载
`onShow(){}`|监听页面显示
`onReady(){}`|监听页面初次渲染完成
`onHide(){}`|监听页面隐藏
`onUnload(){}`|监听页面卸载
`onPullDownRefresh(){}`|监听用户下拉动作
`onReachBottom(){}`|页面上拉触底事件的处理函数
`onShareAppMessage(){}`|用户点击右上角分享


##四、页面路由

* 跳转导航页面：
    ```
    wx.switchTab({
        url: '/pages/index/index'
    })
    ```
* 跳转普通页面：
    ```
    wx.navigateTo({
        url: '/pages/demo/demo'
    })
    ```



**Tips:**
* `navigateTo`, `redirectTo` 只能打开非 `tabBar` 页面。
* `switchTab` 只能打开 `tabBar` 页面。
* `reLaunch` 可以打开任意页面。
* 页面底部的 `tabBar` 由页面决定，即只要是定义为 `tabBar` 的页面，底部都有 `tabBar。`
* 调用页面路由带的参数可以在目标页面的 `onLoad` 中获取。




##五、组件通信
* **父组件：**

    `index.wxml`:
    ```
    <view class='main'>
        <Count id="count" bind:del="del" bind:add="add" testNum="{{testNum}}" />
    </view>
    ```

    `index.json`:
    ```
    {
    "usingComponents": {
        "Count":"/components/count/count",
    },
    "navigationBarTitleText":"父组件页面"
    }
    ```

    `index.js`:
    ```
    const app = getApp()
    Page({
        data: {
            testNum:0
        },
        del(){
            this.setData({
                testNum:--this.data.testNum
            })
        },
        add(){
            this.setData({
                testNum:++this.data.testNum
            })
        },
    })
    ```


* **子组件**
    `count.wxml`:
    ```
    <view class='count'>
        <text>计数器：</text>
        <button bindtap='del'>-</button>
        <text>{{testNum}}</text>
        <button bindtap='add'>+</button>
    </view>   
    ```

    `count.js`:
    ```
    Component({
    /**
    * 组件的属性列表
    */
    properties: {
        testNum:Number//接收父组件传过来的数据
    },

    /**
    * 组件的方法列表
    */
    methods: {
        del(){
        this.triggerEvent('del')//调用父组件方法
        },
        add(){
        this.triggerEvent('add')
        }
    }
    })

    ```


##六、全局变量

`app.js`：
```
App({
  globalData: {
    globalNum:0 //全局变量初始数据
  }
})
```

`index.wxml`:
```
<view class='count'>
    <button bindtap='del'>-</button>
    <text>全局变量：{{testNum}}</text>
    <button bindtap='add'>+</button>
</view>   
```

`index.js`:
```
//获取应用实例
const app = getApp()
Page({
    data: {
        testNum:app.globalData.globalNum,//获取全局变量
    },
    del(){
        app.globalData.globalNum = --app.globalData.globalNum
        this.onShow()//调用页面显示生命周期，全局变量重新赋值刷新页面
    },
    add(){
        app.globalData.globalNum = ++app.globalData.globalNum
        this.onShow()
    },
    /**
    * 生命周期函数--监听页面显示
    */
    onShow: function () {
        this.setData({
            testNum:app.globalData.globalNum
        })
    },
})
```

##七、点击事件
带参：`data-roletype="1"`
```
<view class='roletype' bindtap="roletypeFun" data-roletype="1">
    招工人
</view>
```

列表带参
```
<view class='li' wx:for="{{workArr}}" bindtap="getWork" data-work='{{item}}'>
    {{item.name}}
</view>
```

```
roletypeFun(e){
    console.log(e.target.dataset.roletype)//1
  },
```

##八、样式
绑定动态样式
```
<view class="{{roletype == 1?'roletype_sele':'roletype'}}" bindtap="roletypeFun" data-roletype="1">
    招工人
</view>
```

##九、封装方法
`util.js`:
```
const showToastCom=(config)=>{
  wx.showToast({
    title: config.title || '',
    icon: config.icon || '',
    duration: config.duration || ''
  })
}

module.exports = {
  showToastCom:showToastCom
}
```

`index.js`:
```
import util from '../../utils/util'  //引入

...

click(){
    let config = {
      title: '这里是提示框内容',
      icon: 'none',
      duration: 2000
    }
    util.showToastCom(config)//调用封装方法
},
```