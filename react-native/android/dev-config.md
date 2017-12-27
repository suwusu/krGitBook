# 搭建React Native Mac Android 开发环境 


#### 安装 Homebrew

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

####  安装node

```
brew install node
npm config set registry https://registry.npm.taobao.org --global
npm config set disturl https://npm.taobao.org/dist --global
npm install -g react-native-cli
```


#### 安装 [JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

#### 安装 [Android Studio](https://developer.android.com/studio/index.html)

1. 看到如下页面

![android studio install ](https://reactnative.cn/static/docs/0.43/img/react-native-android-studio-configure-sdk.png)

2. Android sdk buil tools 选用`23.0.1`（很重要)

![android sdk ](https://reactnative.cn/static/docs/0.43/img/react-native-android-studio-android-sdk-build-tools.png)


#### 配置ANDROID_HOME环境变量 (看上图 Android SDK Location 在什么地方，复制)

```
echo "export ANDROID_HOME=~/Library/Android/sdk" >> ~/.bash_profile
source ~/.bash_profile
```

执行｀echo $ANDROID_HOME` 看输出的内容是否正确

#### 其他工具安装

```
brew install watchman
brew install flow
```

##### 提高java编译速度

```
touch ~/.gradle/gradle.properties && echo "org.gradle.daemon=true" >> ~/.gradle/gradle.properties
```


#### 安装 [genymotio]（https://www.genymotion.com/download/） 

#### 安装 [virtualbox]（https://www.virtualbox.org/wiki/Downloads）



#### 测试安装

```
react-native init krDemoApp
cd krDemoApp 
react-native run-android
```




