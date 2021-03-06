---

layout: post
title:  提升开发体验，预览 VirtualView
author: Longerian

---

前面一文介绍了 [VirtualView 工具的更新](http://pingguohe.net/2018/01/23/virtualview-tool.html)，但是我们还需要更加方便的开发体验，比如实时预览。在猫客内，我们配合模板平台，集成了扫码预览的能力。对于开发阶段，我们还需要从模板编译到预览的一条龙服务，因此封装了这么一个小工具。

工具提交在 [github](https://github.com/alibaba/virtualview_tools/tree/master/compiler-tools/TemplateWorkSpace/android-tool)

### 简介
本脚本基于 `buildTemplate.sh` 脚本，整合了『编译』-『上传』-『刷新』的流程。目的在于让模板编写之后自动刷新预览。

### 依赖环境
+ python
+ adb
+ Java

### 使用方法

`python buildAndPreview.py VH2Layout`

参数是模板名称，也就是当前要修改、预览的模板，与 `templatelist.properties` 里的名称一致。

### `previewconfig.conf` 配置参数

+ 推送编译后的 .out 文件到手机存储的路径

```
[path]
target = /sdcard/com.tmall.wireless.virtualviewdemo/virtualview/
```

+ 预览app的预览界面

```
[preview]
activity = com.tmall.wireless.virtualviewdemo.debug/com.tmall.wireless.virtualviewdemo.PreviewActivity
```

以上默认值都是基于 VirtualView-Android 的 [demo](https://github.com/alibaba/Virtualview-Android/) 里配置的，可以自行迁移 demo 代码到自己的 app 环境中进行预览。

默认配置文件：

![](https://user-gold-cdn.xitu.io/2018/3/6/161faebb2ec9d86f?w=761&h=128&f=png&s=5895)

### 预览客户端
默认基于 VirtualView-Android 的 [demo](https://github.com/alibaba/Virtualview-Android/)，当有自定义控件的时候，需要修改预览 app 里，添加自定义组件注册逻辑，因此建议参考 demo 配置自己的预览环境。(注意确保手机有读SD卡权限)

### 演示

![](https://user-gold-cdn.xitu.io/2018/3/6/161fafbe84a817fe?w=800&h=480&f=gif&s=3917418)