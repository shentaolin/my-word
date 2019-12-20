# <center><font>uni-app</font></center>

##一、介绍
uni-app是一个遵循 `Vue` 语法规范的多端开发前端应用框架，**编写一套代码，可以发布到iOS、Android、H5、以及各种小程序（微信/支付宝/百度/头条/QQ/钉钉）等多个平台**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220133448989.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

###1.1定位

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220133612273.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

##二、快速上手
###2.1. 下载编辑器
官方推荐HBuilderX--内置相关环境，开箱即用，无需配置nodejs

###2.2创建uni-app项目
`点击工具栏的文件-->新建-->项目：`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220133850574.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

选择uni-app，输入项目名，如：demo-uniapp，点击创建，即可创建成功（也可通过vue-cli命令行创建项目）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220134021489.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

###2.3运行uni-app项目
1. 浏览器运行，进入demo-uniapp项目，`点击工具栏的运行-->运行到浏览器-->选择浏览器`，即可在浏览器招工体验uni-app的H5版

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019122013455398.png)

2. 真机运行：连接手机，开启USB调试，进入demo-uniapp项目，`点击工具栏的运行-->真机运行-->选择运行的设备`，即可在该设备中体验uni-app

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220134733502.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

3. 在微信开发者工具里运行：进入demo-uniapp项目，`点击工具栏的运行-->运行到小程序模拟器-->微信开发者工具`，即可在微信开发者工具里体验demo-uniapp

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220134905445.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

>其他环境运行情况前往官网查询

###2.4发布uni-app
1. 打包为原生APP
在HBuilderX工具栏，点击发行，选择本地打包，即可生成打包资源

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220135141953.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

2. 发布为微信小程序
先申请微信小程序AppID，再在HBuilderX顶部菜单栏中依次点击：`发行-->小程序-微信`，输入小程序名称和appid，即可在`unpackage\dist\dev\mp-weixin`生成微信小程序项目代码

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220135603935.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220135517290.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

在微信小程序开发者工具中，导入生成的微信小程序项目，测试项目代码运行正常后，点击“上传”按钮，之后按照`提交审核-->发布`小程序标准流程，逐步操作即可

>其他平台发布流程查看uni-app官网

##三、结构组织
###3.1项目结构
一个uni-app项目，默认包含的目录及文件：
```
┌─components            uni-app组件目录
│  └─comp-a.vue         可复用的a组件
├─hybrid                存放本地网页的目录
├─platforms             存放各平台专用页面的目录
├─pages                 业务页面文件存放的目录
│  ├─index
│  │  └─index.vue       index页面
│  └─list
│     └─list.vue        list页面
├─static                存放应用引用静态资源（如图片、视频等）的目录，注意：静态资源只能存放于此
├─wxcomponents          存放小程序组件的目录
├─main.js               Vue初始化入口文件
├─App.vue               应用配置，用来配置App全局样式以及监听 应用生命周期
├─manifest.json         配置应用名称、appid、logo、版本等打包信息
└─pages.json            配置页面路由、导航条、选项卡等页面类信息
```

###3.2页面结构

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220140915359.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

##四、生命周期

###4.1应用生命周期

| 函数名        | 说明   |
-|-|-
| onLaunch      | 当uni-app 初始化完成时触发（全局只触发一次）   |
| onShow        | 当 uni-app 启动，或从后台进入前台显示   |
| onHide        | 当 uni-app 从前台进入后台    |
| onError        | 当 uni-app 报错时触发    |
| onUniNViewMessage        | 对 nvue 页面发送的数据进行监听    |

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220141405359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

>注：应用生命周期仅可在APP.vue中监听，在其他页面监听无效

###4.2页面生命周期

| 函数名        | 说明   |
-|-|-
| onLoad      | 监听页面加载，其参数为上个页面传递的数据，参数类型为Object（用于页面传参）   |
| onShow        | 监听页面显示。页面每次出现在屏幕上都触发，包括从下级页面点返回露出当前页面    |
| onReady        | 监听页面初次渲染完成。注意如果渲染速度快，会在页面进入动画完成前触发    |
| onHide        | 监听页面隐藏    |
| onUnload        | 监听页面卸载    |
| onResize        | 监听窗口尺寸变化    |
| onPullDownRefresh        | 监听用户下拉动作，一般用于下拉刷新    |
| onReachBottom        | 页面上拉触底事件的处理函数    |
| onTabItemTap        | 点击 tab 时触发，参数为Object，具体见下方注意事项    |
| onShareAppMessage        | 用户点击右上角分享    |
| onPageScroll        | 监听页面滚动，参数为Object    |
| onNavigationBarButtonTap        | 监听原生标题栏按钮点击事件，参数为Object    |
| onBackPress        | 监听页面返回    |
| onNavigationBarSearchInputChanged        | 监听原生标题栏搜索输入框输入内容变化事件    |
| onNavigationBarSearchInputConfirmed        | 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。    |
| onNavigationBarSearchInputClicked        | 监听原生标题栏搜索输入框点击事件    |

>平台差异已官网为准

##五、路由
###5.1路由配置
uni-app路由全部交给框架统一管理，在pages.json里配置每个路由页面的路径，不支持`vue router`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220141951256.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)

###5.2路由跳转
uni-app有两种路由跳转方式：
* 使用`navigator`组件跳转`<navigator open-type="navigate"/>`
* 调用API跳转`uni.navigateTo`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191220142129375.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI2Njc2MQ==,size_16,color_FFFFFF,t_70)


---
# End  Loading...  Taro




