# # 学习途径
   ### 1.Effevtive Dart
   >http://dart.goodev.org/guides/language/effective-dart/
# # FLutter-Tips 开发中遇到的点点滴滴记录
### 1.iOS 'Flutter/Flutter.h' file not found
    In file included from /Users/mt/.pub-cache/hosted/pub.flutter-io.cn/flutter_webview_plugin-0.2.1+2/ios/Classes/FlutterWebviewPlugin.m:1:
    /Users/mt/.pub-cache/hosted/pub.flutter-io.cn/flutter_webview_plugin-0.2.1+2/ios/Classes/FlutterWebviewPlugin.h:1:9: fatal error: 'Flutter/Flutter.h' file not found
    #import <Flutter/Flutter.h>
            ^~~~~~~~~~~~~~~~~~~
    1 error generated.
   
这个解决了 大家如果也遇到了 可以尝试
* 在项目根目录运行 flutter clean  
*  删除ios/podfile.lock 再运行

### 2.目前这个版本还存在编译问题，flutter官方也在积极解决
真机运行报错couldn't find "libflutter.so"

暂时的解决方法有：

build.gradle设置

```
ndk{
     abiFilters 'armeabi', 'armeabi-v7a'//, 'arm64-v8a'
}
```

或者可以增加编译选项：

```
--target-platform android-arm64 或者 --target-platform android-arm
```

```
注意~~~~~~~~~~~~~~~~~~~~~~~~~~~了
app/build.gradle文件
defaultConfig节点下

打正式包(加入NDK限制)
        ndk {
            abiFilters 'armeabi-v7a'//'armeabi', 'armeabi-v7a', 'arm64-v8a', 'x86', 'x86_64', 'mips', 'mips64'
        }
打测试包(注释掉NDK代码)
```
### 3.'_InternalLinkedHashMap<dynamic, dynamic>' is not a subtype of type 'Map<String, dynamic>' 
解决办法: ``new Map<String, dynamic>.from(snapshot.value);``

> 引用自:https://github.com/flutter/flutter/issues/16589

### 4.TextField限制字数
如果需要字数提示框 就用``maxLength:11``
如果不需要字数提示框就用 

```
inputFormatters: <TextInputFormatter>[
    WhitelistingTextInputFormatter.digitsOnly,
    LengthLimitingTextInputFormatter(11),
]
```

