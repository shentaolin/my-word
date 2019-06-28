# <center>Vue</center>

##使用Vue-cli 3.0 搭建Vue项目

> ### Vue CLI介绍
> Vue CLI是一个基于Vue.js进行 快速开发的完整系统，提供：
>* 通过`@vue/cli`搭建交互式的项目脚手架
>* 通过`@vue/cli + @vue/cli-service-global`快速开始零配置原型开发
>* 运行时依赖`@vue/cli-service`，该依赖：
>   * 可升级
>   * 基于`webpack`构建，并带有合理的默认配置
>   * 可以通过项目内的配置文件进行配置
>   * 可以通过插件进行扩展
>   * 一个丰富的官方插件集合，集成了前端生态中最好的工具
><p> Vue CLI致力于将Vue生态中的工具基础标准化。它确保了各种构建工具能够基于智能的默认配置即可平稳衔接，这样你可以专注于撰写应用上，而不必花好几天去纠结配置的问题。与此同时，它也为每个工具提供了调整配置的灵活性，无需eject</p>

###环境准备:
####安装Node.js
####安装vue-cli 3.0
> 如果有安装vue-cli旧版本可能会导致安装vue-cli新版本报错
解决方案：
将C:\Users\STL\AppData\Roaming\npm文件下的node_modules文件夹删除，即可重新安装新版本vue-cli
```
npm install -g @vue/cli
```

####vue-cli搭建脚本文件,创建项目(项目名称不能包含大写字母)
>以搭建一个项目名称为vue-demo的Vue前端项目为例
在终端输入一下命令:
```
vue create vue-demo
```
根据提示进行相应的配置（以手动配置为例）：
#####选择`Manually select features`(手动配置)

![Manually select features](https://upload-images.jianshu.io/upload_images/1196972-d73a587f46e9d558.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/650/format/webp "手动配置")

#####选择项目需要的一些特性（此处我们选择需要Babel编译、使用Vue路由、Vue状态管理器、CSS预处理器、代码检测和格式化、以及单元测试，暂时不考虑端到端测试(E2E Testing)）

![texing](https://upload-images.jianshu.io/upload_images/1196972-7b1a2fc2c1779576.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/887/format/webp "特性")

#####选择CSS预处理器语言，此处选择LESS

![less](https://upload-images.jianshu.io/upload_images/1196972-d2be541d362b1662.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/952/format/webp "LESS")

#####选择ESLint的代码规范，此处使用 Standard代码规范

![ESLint](https://upload-images.jianshu.io/upload_images/1196972-cf85c45a5d432058.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/965/format/webp "ESLint代码规范")

#####选择何时进行代码检测，此处选择在保存时进行检测

![lint on save](https://upload-images.jianshu.io/upload_images/1196972-42088b0085a848c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/923/format/webp "代码检测")

#####选择单元测试解决方案，此处选择 Jest

![Jest](https://upload-images.jianshu.io/upload_images/1196972-e631d9f71ab1e18a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/901/format/webp "Jest单元测试")

#####选择 Babel、PostCSS、ESLint等配置文件存放位置，此处选择单独保存在各自的配置文件中

![dedicated config files](https://upload-images.jianshu.io/upload_images/1196972-5dad67c616d6dc0c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/942/format/webp "保存在各自的配置文件")


#####配置完成后等待Vue-cli完成初始化

![Initialize the](https://upload-images.jianshu.io/upload_images/1196972-c27e74c06fadc518.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/826/format/webp "初始化")

#####vue-cli初始化完成后，根据提示，进入到项目vue-demo项目中，并启动项目
```
//进入到vue-demo项目
cd vue-demo
//启动服务
npm run serve
```

###Vue生命周期
* 1.`beforeCreate`
  > 实例创建之前调用
  

* 2.`created`
  > 实例创建成功，此时 data 中的数据显示出来了。
  >在这一步主要的工作为：调用数据，调用方法，调用异步函数。

* 3.`beforeMount`
  > 数据中的 data 在模版中先占一个位置。
  > 在挂载开始之前被调用：render 函数或者模板首次被调用。

* 4.`mounted`
  > 模版中的 data 数据直接显示出来了。
  >`el` 被新创建的 `vm.$el` 替换，并挂载到实例上去之后调用该钩子。这个时候DOM会被渲染完成，初始的数据会被渲染完成，在这里才能获取到具体的DOM元素。

* 5.`beforeUpdate`
  > 数据更新时调用，发生在虚拟 DOM 重新渲染之前。 你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。 当我们更改Vue的任何数据，都会触发该函数。

* 6.`updated`
  > 由于数据更改导致的虚拟 DOM 重新渲染，在这之后会调用该钩子。 当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态，因为这可能会导致更新无限循环。 该钩子在服务器端渲染期间不被调用。

* 7.`beforeDestroy`
  > 实例销毁之前调用。在这一步，实例仍然完全可用。

* 8.`destroyed`
  > Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。 该钩子在服务器端渲染期间不被调用。


###模板语法
`<span>Message: {{ msg }}</span>`
```
<!-- 行内样式： -->
<h1 :style="{color:'red','font-weight':200}">这是一个H1</h1>
```

###Vue指令
Vue 为 `v-bind` 和 `v-on` 这两个最常用的指令，提供了特定简写：

`v-bind` 缩写
```
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>
```

`v-on` 缩写
```
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>
```

####1.`v-bind`:
> `v-bind`指令用于给`html`标签设置属性。
```
<span :text="content">使用</span>

<!-- 会渲染成如下: -->

<span text="content">使用</span>
```

三元表达式：

```
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```
这样写将始终添加 `errorClass`，但是只有在 `isActive` 是 `truthy` 时才添加 `activeClass。`
> `truthy`（真值）指的是在布尔值上下文中，转换后的值为真的值。所有值都是真值，除非它们被定义为 假值（即除 `false`、`0`、`""`、`null`、`undefined` 和 `NaN` 以外皆为真值）。


###2.`v-if`、`v-else`:
> 条件渲染;`v-if` 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 `truthy` 值的时候被渲染。

```
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```
`v-else` 元素必须紧跟在带 `v-if` 或者 `v-else-if` 的元素的后面，否则它将不会被识别。

###3.`v-show`:
> 用法与`v-if`大致一致；不同的是带有 `v-show` 的元素始终会被渲染并保留在 DOM 中。`v-show` 只是简单地切换元素的 CSS 属性 `display`。

```
<h1 v-show="error">Error!</h1>
...
data(){
  return{
    error:false
  }
}

<!-- 会渲染成如下: -->

<h1 style="display: none;">Error!</h1>
```

###4.`v-for`:
> 可以用 `v-for` 指令基于一个数组来渲染一个列表;
`v-for`具有比 `v-if` 更高的优先级

```
<ul id="example-1">
  <li v-for="(item, index) in items">
    {{ index }}:{{ item.message }}
  </li>
</ul>
...
data(){
  return{
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
}
```

也可以用 `of` 替代 `in` 作为分隔符，因为它更接近 `JavaScript` 迭代器的语法：
`<div v-for="item of items"></div>`

也可以用 `v-for` 来遍历一个对象的属性:
```
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
...
data(){
  return{
    object: {
      title: 'How to do lists in Vue',
      author: 'Jane Doe',
      publishedAt: '2016-04-10'
    }
  }
}
```

也可以提供第二个的参数为 `property` 名称 (也就是键名)：
```
<div v-for="(value, name) in object">
  {{ name }}: {{ value }}
</div>
```

还可以用第三个参数作为索引：
```
<div v-for="(value, name, index) in object">
  {{ index }}. {{ name }}: {{ value }}
</div>
```

###5.`v-on`:
> 用 `v-on` 指令监听 DOM 事件
`<button v-on:click="counter += 1">Add</button>`

```
<div id="example-2">
  <!-- `greet` 是在下面定义的方法名 -->
  <button v-on:click="greet">Greet</button>
</div>
```

####事件修饰符
>修饰符是由点开头的指令后缀来表示的。
* `.stop`
* `.prevent`
* `.capture`
* `.self`
* `.once`
* `.passive`

```
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

>使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。
因此，用 `v-on:click.prevent.self` 会阻止所有的点击，
而 `v-on:click.self.prevent` 只会阻止对元素自身的点击。

###6.`v-model`:
>可以用 `v-model` 指令在表单 `<input>`、`<textarea>` 及 `<select>` 元素上创建双向数据绑定。

`v-model` 会忽略所有表单元素的 `value、checked、selected` 特性的初始值而总是将 Vue 实例的数据作为数据来源。你应该通过 `JavaScript` 在组件的 `data` 选项中声明初始值。

```
<input v-model="message" placeholder="edit me">
<p>Message is: {{ message }}</p>
```

##父子组件
1.父 => 子（传值）
```
<!-- 父组件： -->
静态值：title = 'My Journey with Vue'
动态值：v-bind:title="post.title"
...
post: {
  title: 'My Journey with Vue'
}

<!-- 子组件： -->
<span>{{title}}</span>
...
<!-- 这个 prop 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 prop 数据来使用。在这种情况下，最好定义一个本地的 data 属性并将这个 prop 用作其初始值： -->
props:['title'],
```

2.子 => 父（传值）
```
<!-- 父组件： -->
@childFn="parentFn"
子组件传来的值 : {{message}}
...
data: {
    message: ''
},
methods: {
    parentFn(payload) {
    this.message = payload;
  }
}

<!-- 子组件： -->
<input type="text" v-model="message" />
<button @click="click">Send</button>
...
data() {
    return {
      // 默认
      message: '我是来自子组件的消息'
    }
},
methods: {
  click() {
        this.$emit('childFn', this.message);
    }
}   
```

3.父 => 子（传方法）
```
<!-- 父组件： -->
<child @fatherMethod="fatherMethod"></child>
...
method:{
    fatherMethod(){
        //方法体
    }
}

<!-- 子组件： -->
<button @click="childMethod()">点击</button>
...
methods: {
    childMethod() {
        this.$emit('fatherMethod');  //使用$emit()引入父组件中的方法
    }
},
```

4.子 => 父（传方法）
```
<!-- 父组件： -->
button v-on:click="clickParent">点击</button>
<child1 ref="child1"></child1>
...
methods: {
    clickParent() {
        this.$refs.child1.handleParentClick("val");//val为子组件传给父组件的值
    }
}

<!-- 子组件： -->
methods: {
    handleParentClick(e) {
    }
}
```







##Vuex
> 新建一个store.js：
```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    storeMsg:'store计数器',
    storeCount:0
  },
  mutations: {
    del(state,payload){
      state.storeCount--
    },
    add(state,payload){
      state.storeCount++
    }
  },
  actions: {

  }
})
```
actions为数据请求方法，例fun函数：
```
fun(context,payload){
  ...数据请求
  context.commit('mutations方法名',参数)
}
```
Action 通过 store.dispatch 方法触发：
```
store.dispatch('increment')
```

>vue模板文件：
```
<template>
  <div class="storeCount">
    <span>{{storeMsg}}：</span>
  
    <button class="btn" @click="del()">-</button>
    <span class="count">{{storeCount}}</span>
    <button class="btn" @click="add()">+</button>

  </div>
</template>

<script>
import {mapState,mapMutations,mapActions} from 'vuex';
export default {
  name: "vue",
  data() {
    return {
    };
  },
  computed:{
      ...mapState(['storeMsg','storeCount'])
  },
  methods: {
      ...mapMutations(['add','del']),
      <!-- ...mapActions('命名空间',['action方法名']) -->
  }
};
</script>
```

##iframe高度自适应
```
<iframe width="100%" src="http://localhost:8080/" frameborder="0" scrolling="no" id="iframepage" onload="changeFrameHeight()"></iframe>

...

function changeFrameHeight(){
    var ifm= document.getElementById("iframepage"); 
    ifm.height=document.documentElement.clientHeight;
}
window.onresize=function(){  
     changeFrameHeight();  
}

```


##Element安装
```
npm i element-ui -S
```

##引入Element
>完整引入

在 main.js 中写入以下内容：
```
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
```
##Element
###输入框:
`trigger: 'blur'` 标识当是去焦点时（光标不显示的时候）触发提示

####[输入框输入限制，正则判断：](https://blog.csdn.net/redwolfchao/article/details/84973177)
> 只能输入数字：`oninput="value=value.replace(/[^\d]/g,'')"`
```
<el-input
    v-model.number="ruleForm.number"
    placeholder='请输入6位以内数字'
    maxlength="6"
    oninput="value=value.replace(/[^\d]/g,'')"
></el-input>
```

> 只能输入字母和汉字：`oninput="value=value.replace(/[\d]/g,'')"`
> 只能输入字母和汉字和数字：`oninput="value=value.replace(/[^\w\u4E00-\u9FA5]/g,'')"`

