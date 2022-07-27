# ZXKitCore

![](https://img.shields.io/badge/CocoaPods-supported-brightgreen) ![](https://img.shields.io/badge/Swift-5.0-brightgreen) ![](https://img.shields.io/badge/License-MIT-brightgreen) ![](https://img.shields.io/badge/version-iOS11.0-brightgreen)

[English](./README_en.md)

`ZXKitCore`是ZXKit插件的支撑框架，提供了插件显示、管理等功能，只需要实现对应的`ZXKitPluginProtocol`协议，即可快速的开发出ZXKit插件并显示使用。该文档提供了插件开发教程和使用教程，开发者可以根据需要查看。

> 天地不仁，以万物为刍狗 		
>  -诛仙


## 开发一个ZXKit插件

如果需要开发自定义插件，只需要实现`ZXKitPluginProtocol`即可。实现的方式很简单。

### 1、导入核心文件

项目导入`ZXKitCore`，可使用cocoapods快速导入核心文件

```
pod 'ZXKitCore/core'
```

### 2、实现协议

声明一个对象，遵守`ZXKitPluginProtocol`协议即可。分别返回对应插件的唯一标识，对应的icon、插件名字、插件类型分组、启动函数

```
class PluginDemo: NSObject {
    var isPluginRunning = true
}

extension PluginDemo: ZXKitPluginProtocol {
	 //唯一标识
    var pluginIdentifier: String {
        return "com.zxkit.pluginDemo"
    }
    
    var pluginIcon: UIImage? {
        return UIImage(named: "zxkit")
    }

    var pluginTitle: String {
        return "插件标题"
    }

    var pluginType: ZXKitPluginType {
        return .ui
    }

    func start() {
        print("点击启动该插件")
        isPluginRunning = true
    }
    
    var isRunning: Bool {
        return isPluginRunning
    }

    func stop() {
        print("插件停止运行")
        isPluginRunning = false
    }
}
```

### 3、注册插件

之后注册插件即可，全局只需注册一次即可

```
ZXKit.regist(plugin: PluginDemo())
```

### 4、完成

cocoapods发布上线之后，当用户打开`ZXKit`时，调试集合页就会出现您的插件

### 5、更多属性

#### 5.1、获取悬浮的按钮对象

```
ZXKit.floatButton
```

#### 5.2、还原悬浮按钮的样式

```
ZXKit.resetFloatButton()
```

#### 5.3、显示输入框

```
ZXKit.showInput { (text) in
	print(text)
}
```

#### 5.4、获得输入框对象

```
ZXKit.textField
```

### 消息通知

`ZXKitCore`提供了以下消息通知，您可以通过绑定以下通知获取框架显示、隐藏、关闭、注册新插件的时机

```
//注册新插件
NSNotification.Name.ZXKitPluginRegist
//显示
NSNotification.Name.ZXKitShow
//隐藏
NSNotification.Name.ZXKitHide
//关闭
NSNotification.Name.ZXKitClose
```

## 安装使用ZXKit插件

`ZXKit`插件使用很简单，只需要导入对应的库，在`AppDelegate`启动函数注册即可。例如安装`日志插件ZXKitLogger`。

### 首先pod安装对应插件

```
pod 'ZXKitLogger/zxkit'
```
### 注册插件

```
ZXKit.regist(plugin: ZXKitLogger.shared)
```

### 打开插件列表

```
ZXKit.show()
```

### 隐藏插件列表

```
ZXKit.hide()
```

### 关闭插件列表

```
ZXKit.close()
```

## ZXKitSwift

我们发布了一个cocoaPods库，名字叫[ZXKitSwift](https://github.com/ZXKitCode/ZXKitSwift)，这是一个集成了多个ZXKit插件的工具库。可以帮助你快速使用多个调试功能。

## License

ZXKitCore 基于 MIT license 发布。
