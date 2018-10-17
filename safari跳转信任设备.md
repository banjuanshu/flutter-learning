# Safari 跳转至信任设备

### URL Scheme
```
iOS 9 : prefs:root=General&path=ManagedConfigurationList
iOS 10 : App-Prefs:root=General&path=ManagedConfigurationList
```

#### 解决

可以看到 iOS10 并不能从 Safari 直接跳转 [描述文件] 页面了，但是还有一个方式可以达到该效果，那就是直接链接到一个企业签名的描述文件(.mobileprovision)，在 Safari 中直接访问 http://www.banjuanshu.com/app.mobileprovision 就可以实现跳转了。


* 从到苹果开发者的证书管理中，下载企业发布证书 xxx.mobileprovision。
* 把证书放到服务器上
* href 改为证书在服务器上的路径

