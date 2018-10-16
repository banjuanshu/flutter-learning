# flutter-learning
flutter 学习整理

"${PODS_CONFIGURATION_BUILD_DIR}/shared_preferences"
"${PODS_CONFIGURATION_BUILD_DIR}/shared_preferences"


### 错误

```
ld: warning: directory not found for option '-L/Users/bjs/pro/haoyoulv/ft/build/ios/Debug-iphoneos/shared_preferences'
ld: library not found for -lshared_preferences
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

```
打开 `.xcworkspace`文件,然后运行
```



### 创建 model

```
flutter packages pub run build_runner build
```

* 创建错误

```
flutter packages pub run build_runner build --delete-conflicting-outputs
```


* type 'String' is not a subtype of type 'Map<dynamic, dynamic>'

```
// 网络返回的json先要用json.decode 反转一下

import 'dart:convert';

jsonStr = json.decode(jsonStr);


```

