# <center><font color='blue'>环境搭建</font></center>

## 一、 安装依赖
必须安装的依赖有：Node、Python2 以及 JDK 、React Native 命令行工具和 Android Studio。

### 1. [官网](https://nodejs.org/zh-cn/)下载安装Node（Node 的版本必须高于 8.3）
### 2. [官网](https://www.python.org/)下载安装Python2（版本必须为 2.x）
### 3. [官网](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下载安装JDK（版本必须是 1.8）

#### jdk配置（右键偶的电脑—属性—高级系统设置—环境变量）：
①. 创建一个名为ANDROID_HOME的环境变量（系统或用户变量均可），指向你的 Android SDK 所在的目录

![](https://user-gold-cdn.xitu.io/2019/4/20/16a3b655c8bdf140?w=468&h=118&f=png&s=19252)

②. 把platform-tools目录添加到环境变量Path中
③. 接下来配置JAVA_HOME(缺了这一步Android studio会显示找不到jdk安装目录，路径不包含bin文件)


```
    新建变量：JAVA_HOME
    变量值：JDK安装目录
```

![](https://user-gold-cdn.xitu.io/2019/4/20/16a3b69504f78c23?w=468&h=131&f=png&s=23179)

④. 在系统变量里寻找 Path 变量，选择编辑，新建两个变量值`%JAVA_HOME%\bin，%JAVA_HOME%\jre\bin`

![](https://user-gold-cdn.xitu.io/2019/4/20/16a3b6ab44dc3340?w=468&h=499&f=png&s=98190)

⑤. 新建环境变量，命名为`CLASSPATH`，变量值填入`.;%Java_Home%\bin;%Java_Home%\lib\dt.jar;%Java_Home%\lib\tools.jar `

⑥. 记得配置（官网无记录）：`JRE_HOME`    `C:\Program Files\Java\jre7`（根据jdk安装位置更改路径）

jdk安装且环境配置完成，可在cmd中检查是否安装成功，命令：`java -version`


### 4. React Native命令行工具（react-native-cli）安装：`npm install -g yarn react-native-cli`

### 5. 安装Android Studio

## 二、 Android开发环境
### 1. [安装翻墙工具](https://github.com/shadowsocks/shadowsocks-windows)

![](https://user-gold-cdn.xitu.io/2019/4/21/16a3bcebe978c14a?w=468&h=509&f=png&s=115648)

### 2. 安装Android SDK
Android Studio默认会安装最新版本的Android SDK

①. 在 Android Studio 的欢迎界面中找到 SDK Manager（右下角选项）。点击`Configure`，然后就能看到`SDK Manager`。

②. 在 SDK Manager 中选择`SDK Platforms`选项卡，然后在右下角勾选`Show Package Details`。展开Android 9 (Pie)选项，确保勾选了下面这些组件（重申你必须使用稳定的翻墙工具，否则可能都看不到这个界面）
* `Android SDK Platform 28`
* `Intel x86 Atom_64 System Image（官方模拟器镜像文件，使用非官方模拟器不需要安装此组件）`

③. 然后点击`SDK Tools`选项卡，同样勾中右下角的`Show Package Details`。展开`Android SDK Build-Tools`选项，确保选中了 React Native 所必须的28.0.3版本。你可以同时安装多个其他版本。
最后点击"Apply"来下载和安装这些组件。

### 3. 配置ANDROID_HOME环境变量
打开控制面板 -> 系统和安全 -> 系统 -> 高级系统设置 -> 高级 -> 环境变量 -> 新建，创建一个名为`ANDROID_HOME`的环境变量（系统或用户变量均可），指向你的 Android SDK 所在的目录（SDK 默认是安装目录：`c:\Users\你的用户名\AppData\Local\Android\Sdk`）

### 4. 把 platform-tools 目录添加到环境变量 Path 中
打开控制面板 -> 系统和安全 -> 系统 -> 高级系统设置 -> 高级 -> 环境变量，选中`Path`变量，然后点击编辑。点击新建然后把 platform-tools 目录路径添加进去（此目录的默认路径为：`c:\Users\你的用户名\AppData\Local\Android\Sdk\platform-tools`）。
> <font color='red'>注：添加目录路径要和之前path已有路径用分号分割</font>

## 三、创建新项目
使用 React Native 命令行工具来创建一个名为"demo"的新项目：`react-native init demo`
> 创建指定RN版本项目：
`react-native init demo --verbose --version 0.44.0(版本号)`

## 四、编译并运行React Native应用
> 进入项目`cd demo`

> 运行项目`react-native run-android`

# <center><font color='blue'>link问题</font></center>

## 引入navigation
1. 在 React Native 项目中安装react-navigation这个包:  `npm install --save react-navigation`
2. 安装 react-native-gesture-handler:  `npm install --save react-native-gesture-handler`
3. Link 所有的原生依赖:  `react-native link react-native-gesture-handler`

## 相关配置文件
1. android>settings.gradle
```
include ':react-native-gesture-handler'
project(':react-native-gesture-handler').projectDir = new File(rootProject.projectDir,
'../node_modules/react-native-gesture-handler/android')
```
2. android>app>build.gradle
```
dependencies {
    implementation project(':react-native-gesture-handler')
    implementation fileTree(dir: "libs", include: ["*.jar"])
    implementation "com.android.support:appcompat-v7:${rootProject.ext.supportLibVersion}"
    implementation "com.facebook.react:react-native:+"  // From node_modules
}

```
3. android>app>src>main>java>com>MainApplication.java
```
import com.swmansion.gesturehandler.react.RNGestureHandlerPackage;
```
```
@Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
            new RNGestureHandlerPackage(),
      );
    }
```
4. android>app>src>main>java>com>MainActivity.java
```
import com.swmansion.gesturehandler.react.RNGestureHandlerEnabledRootView;
```
```
@Override
    protected ReactActivityDelegate createReactActivityDelegate() {
        return new ReactActivityDelegate(this, getMainComponentName()) {
            @Override
            protected ReactRootView createRootView() {
                return new RNGestureHandlerEnabledRootView(MainActivity.this);
            }
        };
    }

```

## 注意链接原生依赖（react-native link）时的坑
#### 1. 链接原生库`react-native  link`后，注意android>app>src>main>java>com> MainApplication.java文件里面,有没有重复，如下：
```
@Override
protected List<ReactPackage> getPackages() {
    return Arrays.<ReactPackage>asList(
        new MainReactPackage(),
        new RefreshReactPackage(),
        new RNGestureHandlerPackage()
    );
}
```
你执行函数的命令因为重复执行link命令重复添加了，手动删除多余的即可；

还有settings.gradle也会出现多余的

#### 2. android\settings.gradle文件中反斜杠更改：

> 错例：

```
project(':react-native-linear-gradient').projectDir = new File(rootProject.projectDir, '..\node_modules\react-native-linear-gradient\android')
```

#### 3. 错误提示效果:app:compileDebugJavaWithJavac
解决：用android studio打开项目进行编译后再重新运行项目即可；

* 使用android studio打开android文件即可（而不是打开整个文件）
* 如果还是报错：将项目android文件下的 ***.iml    文件删掉，重新导入编译即可

## 手动link配置
> 例：配置react-native-image-picker（一个集成相机和相册的功能的第三方库）示例：

react-native-image-picker使用

1. 首先,安装下该插件`npm install react-native-image-picker@latest --save`
2. 针对Android和iOS平台分别进行配置:

> #### android 平台配置

1. 在android/settings.gradle文件中添加如下代码：
```
include ':react-native-image-picker'
project(':react-native-image-picker').projectDir = new File(settingsDir, '../node_modules/react-native-image-picker/android')

```

2. 在android/app/build.gradle文件的dependencies中添加如下代码：
```
compile project(':react-native-image-picker')
```

3. 在AndroidManifest.xml文件中添加权限：
```
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

4. 最后在MainApplication.Java文件中添加如下代码：
```
import com.imagepicker.ImagePickerPackage;
 new ImagePickerPackage()
```
这样Android环境就配置好了。

> #### iOS平台配置

1. 打开Xcode打开项目,点击根目录,右键选择　Add Files to ‘XXX’,选中项目中的该路径下的文件即可:node_modules -> react-native-image-picker -> ios -> select RNImagePicker.xcodeproj
2. 添加成功后使用link命令：react-native link react-native-image-picker 。
3. 打开项目依次使用Build Phases -> Link Binary With Libraries将RNImagePicker.a添加到项目依赖。
4. 对于iOS 10+设备，需要在info.plist中配置NSPhotoLibraryUsageDescription和NSCameraUsageDescription。


# <center><font color='blue'>前端RN打包</font></center>
在 Android Studio 中打包，即生成离线的 jsbundle 文件：

```
react-native bundle --platform android --dev false --entry-file index.android.js --bundle-output app/src/main/assets/index.android.bundle --assets-dest app/src/main/res/
```
> 路径解析：

`index.android.js`：打包生成的文件

`app/src/main/assets/index.android.bundle`：打包生成文件所在目录

`app/src/main/res/`：RN中用到的静态资源文件打包后生成文件所在目录
