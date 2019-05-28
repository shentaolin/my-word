# <center>RN笔记</center>

####调试
打开开发者菜单--进入`Dev Settings`--点击`Debug server host for device`--输入你电脑的IP地址和端口号（譬如10.0.1.1:8081）

####引入图片
```
<Image style={styles.menuimg} source={{uri:'http://nm.jgjapp.com/public/imgs/job/my-job.png'}}></Image>
```

####平台判断
```
if (Platform.OS == 'android' ||  Platform.OS == 'ios') {
    //android
}else{
    //ios
}
```

####android页面跳转
```
if (Platform.OS == 'android') {//android端
    NativeModules.MyNativeModule.openWebView(跳转地址);//调用原生方法
}
```

####android方法调用
```
NativeModules.MyNativeModule.openRepository();//调用原生方法
```

####RN属性
>Text显示单行内容，多余用省略号显示`numberOfLines={1}`


>RN按钮点击透明度设置`activeOpacity={1}`

>RN按钮点击改变样式
```
TouchableNativeFeedback
background={TouchableNativeFeedback.Ripple('#e4e4e4',false)}
```

>Text字体大小随系统变化
```
解决方案，改源码：
node_modules/react-native/Libraries/Text/Text.js`文件，
allowFontScaling: false,设置为false
```

>【React Native】 Android环境下TextInput设置textAlign后导致ScrollView滚动不正常

```
解决方案:
multiline = {true}
keyboardType = {“default”} 
并限制`maxLength`可暂时解决此问题
```

####RN存储
```
// 存
AsyncStorage.setItem('ppbz', JSON.stringify(res), (error) => {
    if (error) {
        // alert('存储失败');
    } else {
        // alert('存储成功');
    }
});

// 取
AsyncStorage.getItem('ppbz', (error, result) => {
    if (!error) {
        // console.log(result);
        this.setState({
            dataSource: JSON.parse(result)
        })
    }
})
```

####关闭黄屏警告
```
入口文件index.js加入：
console.ignoredYellowBox = ['Warning: BackAndroid is deprecated. Please use BackHandler instead.','source.uri should not be an empty string','Invalid props.style key'];
console.disableYellowBox = true // 关闭全部黄色警告
```


