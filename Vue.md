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

