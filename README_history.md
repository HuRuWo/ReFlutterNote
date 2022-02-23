## ReFlutterNote(逆向flutter笔记)

## 前言

鉴于目前越来越多软件采用flutter进行开发，导致逆向安全难度增大。
所以在连续分析了一些颜色APP软件之后，我准备分享一些相关的逆向知识。做抛砖引玉之用。

## 章节目录

>所有内容都是以release版本为逆向对象，debug版本没啥看的。没有人会发布debug版本的软件到应用市场。

>年底业务繁忙，工程笔记慢速施工当中。

### 0.flutter 的基本开发


在进入逆向之前，我们先做一点正向的开发。方便我们理解和思考后续的进入。

这里我们进行简单的crackme程序开发。

#### 环境搭建f

[flutter逆向从自信入门到精通跑路系列1-flutter编程环境搭建](https://www.huruwo.top/flutter%e9%80%86%e5%90%91%e4%bb%8e%e8%87%aa%e4%bf%a1%e5%85%a5%e9%97%a8%e5%88%b0%e7%b2%be%e9%80%9a%e8%b7%91%e8%b7%af%e7%b3%bb%e5%88%971-flutter%e7%bc%96%e7%a8%8b%e7%8e%af%e5%a2%83%e6%90%ad%e5%bb%ba/)

#### 新建项目和编写crackme


[flutterdart逆向从自信入门到精通跑路系列2-编写crackme](https://www.huruwo.top/flutterdart%e9%80%86%e5%90%91%e4%bb%8e%e8%87%aa%e4%bf%a1%e5%85%a5%e9%97%a8%e5%88%b0%e7%b2%be%e9%80%9a%e8%b7%91%e8%b7%af%e7%b3%bb%e5%88%972-%e7%bc%96%e5%86%99crackme/)


进入基本的开发之后 进入后续的逆向过程


### 1.flutter apk结构

在前面的基本开发过程中,我们得到了一个较为简单的flutter apk 文件。现在我们来将其解析分析里面包含的文件内容。


```
F:\flutter\bin\flutter.bat --no-color build apk
Running Gradle task 'assembleRelease'...                          114.7s
√  Built build\app\outputs\flutter-apk\app-release.apk (16.5MB).
Process finished with exit code 0
```

整个apk大小挺恐怖的，我们之前只写了几行代码几个类居然有16.5MB的大小。

![](pic/01.png)

原因是在lib里面用了三套架构，我们只保留一套即可

```
defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.example.fluttertest"
        minSdkVersion 16
        targetSdkVersion 30
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName

        ndk {
            abiFilters "armeabi-v7a" //架构保留
        }

    }
```

```
F:\flutter\bin\flutter.bat --no-color build apk

 Building with sound null safety 

Running Gradle task 'assembleRelease'...                            5.4s
√  Built build\app\outputs\flutter-apk\app-release.apk (5.4MB).
Process finished with exit code 0
```

这下我们的apk只有5.4M

![](pic/02.png)

关于flutter的部分在

lib asset 两个文件夹里面，asset存放的就是相关的资源文件而lib里面就存放了我们要破解的flutter的代码。

- libflutter.so 完整的flutter虚拟机

- libapp.so     flutter程序代码对应的dart vm AOT 快照文件


### 2.dart 虚拟机架构

接下我们要进入有些难度的虚拟机架构相关内容，这一部分有些难度。

而且flutter版本在快速迭代中。所以我不能保证现在版本的虚拟机依然是这样子的。

好在有几篇非常重要的研究文章在网络上可以找到,我列举出来作为参考。

flutter的so中包含着一个dart语言的虚拟机，因为flutter本身还要和安卓系统交互进行ui相关的绘制。所以flutter lib 中包含的内容是要大于dart虚拟机的。

为了了解dart语言的运行，了解dart虚拟机的构成也是非常必要的。








### 3.dart AOT 快照文件格式

### 4.flutter 数据包抓取方式

>这里补充一个关于flutter应用的抓白方案。鉴于flutter不会通过代理方式进行通信，通常使用的


### 5.flutter SDK 引擎编译

### 6.flutter SDK 引擎注入重打包

### 7.flutter AOT快照解析

### 8.flutter function code 定位

### 9.flutter function code 修改

### 10.flutter frida hook

### 11.flutter frida xposed hook

### 12.flutter dart 算法还原

### 13.flutter 更多相关知识点 

## 最后

如有有需求的可以帮忙点点start让我知道有人在看。我会更快的抽出时间来更新教程。

如果有帮助,各位手动点点start即可。有问题直接issue讨论或者邮件联系我。

