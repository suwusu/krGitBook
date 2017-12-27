# 生成 app

>[参考文档](http://reactnative.cn/docs/0.26/signed-apk-android.html#%E5%A6%82%E6%9E%9C%E4%BD%A0-%E6%B2%A1%E6%9C%89-react-gradle-%E6%96%87%E4%BB%B6-)

#### 生成已签名的APK

```
keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

#### 设置gradle变量

1. 把my-release-key.keystore文件放到你工程中的android/app文件夹下。
2. 编辑~/.gradle/gradle.properties，添加如下的代码（注意把其中的****替换为相应密码）

```
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=*****
MYAPP_RELEASE_KEY_PASSWORD=*****
```


#### 添加签名到应用的gradle配置文件
>编辑你工程目录下的android/app/build.gradle，添加如下的内容：

```
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            storeFile file(MYAPP_RELEASE_STORE_FILE)
            storePassword MYAPP_RELEASE_STORE_PASSWORD
            keyAlias MYAPP_RELEASE_KEY_ALIAS
            keyPassword MYAPP_RELEASE_KEY_PASSWORD
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...
```


#### 生成发行APK包
>如果你在android/app下有一个react.gradle

只要在终端下运行以下命令：

```
 cd android && ./gradlew assembleRelease
```

#### 测试应用的发行版本

```
cd android && ./gradlew installRelease
```

