今年 WWDC 大会有哪些新技术？"

> 作者：Olivier Halligon，[原文链接](http://alisoftware.github.io/conferences/2016/06/20/ios-10-api-diff/)，原文日期：2016-06-20
> 译者：[Crystal Sun](http://www.jianshu.com/users/7a2d2cc38444/latest_articles)；校对：[numbbbbb](http://numbbbbb.com/)；定稿：[千叶知风](http://weibo.com/xiaoxxiao)
  









好吧，好悲伤，我今年没能参加 WWDC 大会 😢，只能看视频 🎥 和 Twitter。我打赌你们肯定都看了发布会的重要内容（至少看了 keynote）和各个平台的新动态 🎉。不过你知道那些悄悄加进去的新 API 吗？🕵

## 列出这个清单的目的

每年 WWDC 的问题就是会发布成吨的信息、通知、视频，以至于都没有时间来观看和体验所有东西！

列这个清单并不是想让你看到精疲力尽，只是帮你发现一些你可能会遗漏的主题。有了这个清单，你就能够决定花时间看哪些 WWDC 的视频、阅读哪些文档、以及在 playground 里体验哪些新的 API...当然前提是你有时间。



> 过段时间我可能会给这个清单添加 🎬WWDC 视频编号，链接到对应的会议或者博客文章，不过现在我还不想让我的清单变得太长😉
 
## 新 API

### 语音识别

新的 `SFSpeechRecognizer` 框架，可以分析语音内容，支持语音转文字。

### SiriKit

好吧，估计你已经看过这个了。不过我还是添加到清单里了，因为等我有时间的时候想实践一下。

借助 SiriKit，应用能够识别具体的静态或者动态的词汇。借助 interpreted meta-data（`Intent`）Siri 能够调用你的应用，使用一些功能。

> 👀 [Programming Guide](https://developer.apple.com/library/prerelease/content/documentation/Intents/Conceptual/SiriIntegrationGuide/index.html##//apple_ref/doc/uid/TP40016875)，[Intents.framework](https://developer.apple.com/reference/intents) 和 [IntentsUI.framework](https://developer.apple.com/reference/intentsui) 
  🎬 #217
  
### 精致的通知框架

 - 统一本地和远程通知
 - 在通知里可以加入多媒体内容，比如图片和 GIF 图片
 - 当用户禁止通知时，你会收到告知
 - 能够获得你应用里的通知清单，能够控制触发时间，能更新这些通知，甚至具备删除旧通知的能力
 - [通过代码可以获取用户的通知设置情况](https://twitter.com/NatashaTheRobot/status/744506324696760320)
 
> 👀`UserNotifications.framework` 和 `UserNotificationsUI.framework` 文档
 
### CloudKit

支持 CloudKit 的分享操作，会显示一个界面让用户浏览和修改参与者、开始分享和结束分享。

> 👀`UICloudSharingController` 和 `UICloudSharingControllerDelegate`
> 还可以在 iOS 10 的 Notes.app 看到

### CoreGraphics

API 会 Swift 化，C 语言风格的 API 已经一去不复返，现在可以在 CoreGraphic API 里用 `context.xxx()` 代替 `CGContextXXX()` 了。

### Foundation

**日期**

 - `NSISO8601DateFormatter` 终于正式出现在 Foundation 里了！
 - 有了新的 `NSDateInterval` 类型

**单位转换**

这是新的 API，能够转换各种不同的测量单位。
 
**对 API 做去字符串化（De-stringification）**

 - `NSCalendarIdentifier` 现在已经是一个专门的类型了（代替了 `NSString`）
 - `NSError.domain` 现在是一个 `NSErrorDomain`，代替了 `NSString`
 - 通知里使用 `NSNotificationName` 代替 `NSString`
 - `stringByApplyingTransform:reverse:` 使用 `NSStringTransform` 类型代替 `NSString`
 - `NSRunLoop.mode` 现在是一个 `NSRunLoopMode`，代替了……额你猜？
 - `NSHTTPCookie` 属性现在是 `[NSHTTPCookiePropertyKey: AnyObject]`，代替了 `[NSString: AnyObject]`
 - 诸如此类
  
**新的日志 API**

全局函数 `os_log`，有不同的日志级别，等等。

**New timer API**

现在可以传入闭包了！（*Xcode 8 的 Swift 还不支持这个功能，会在 Swift 3 加入。*）

    Timer(fireDate: when, interval: 0, repeats: false) { /* code */ }

**NSURLSession**

新的委托方法允许你获取一些网络相关的数据。提供了很多元数据，比如不同场景的开始和结束时间（DNS 查询、连接……）

> 👀` NSURLSessionTaskMetrics` 和 `NSURLSessionTaskTransactionMetrics`

### UITableView 和 UICollectionView 预加载

 - 预加载：在到达滑动区域的边缘之前预先下载数据，更轻松地实现多页内容。
 - `UIRefreshControl` 目前已经可以在 `UIScrollView` 上使用了（之前只能在 `UITableViewController` 上使用）。
 - 新的 `UICollectionViewFlowLayoutAutomaticSize` CollectionView 约束条件！

### GCD

新的 `Dispatch` API 出现在 Swift 3 里，用于 GCD（Grand Central Dispatch）。在 Swift 3 里操作 GCD 更容易也更美观！
 
### UUID 值类型

在 Swift 3 里出现了一个新的类型 `UUID`，是一个值类型（估计和 Objective-C 里的 `NSUUID` 类似）。

### UIViewPropertyAnimator

新的 `UIViewPropertyAnimator` 类可以更好地使用 `UIView.animatedWithDuration` API，借此可以实现很多功能，比如：
 
 - 中途中断动画
 - 动画开始后改变值
 - 改变 `percentComplete` 属性让动画更具交互性
 - 或者甚至可以把 `percentComplete` 和 `UIGestureRecognizer` 结合在一起使用

### UIPasteboard

 - `UIPasteboard` 现在能够 **在不同的设备之间共享同一个剪贴板**，例如：你在 Mac 上复制了一段话，然后粘贴到你的 iPhone/iPad 上，反过来也可以。

### UITabBar

 - 能够控制一个 tab bar item 的样式，比如背景颜色和文字属性。

### CoreData

 - 更好的适配 Swift
 - 更好的数据获取方式和错误处理
 - 更紧密地集成到 Xcode 中，优化生成过程，支持**更新** `NSManagedObject` 子类。

### ApplePay

 - 苹果支付现在支持网页支付啦（仅限 Safari 10）
 - 支持更多新的国家（包括我所在的 🇫🇷！）（译者注：作者是法国的）

### Messages API

 - 新的框架，用于创建基于 iMessage 的新应用
 - 能够创建 iMessage 的表情包

## watchOS 3

我不是一个 watchOS 开发者，所以我可能会多看几次这部分的知识点，我注意到 watchOS 3 有：
 
 - 更短的启动时间
 - 没有了 Glance，换成了 App Switcher
 - 更新 API 可以截屏 App Swifter
 - 可以访问 digital crown（数码表冠）了，还可以获取陀螺仪的事件

## tvOS
 - 结合 SSO（Single SignOn），能够更轻松的管理 tvOS 上应用的密码，更快地登录。
 - 在 tvOS 10 上，焦点触发 textField 后，[在你的 iPhone/iPad 上会出现文本通知](https://twitter.com/olebegemann/status/744881057208602624)，你的 iPhone/iPad 可以当做远程键盘使用。

 
## Xcode 里的新工具

 - 新的可视化调试工具（Visual Debugging Tools），特别是内存和线程工具
 - 新的代码签名机制
 - Xcode 扩展
 - 在 Xcode 8 里允许你选择使用 Swift 2.3 还是 Swift 3.0
 - 修订文档
 - 图片名字自动补全，代码中可以对颜色和图片文字化
 - 提高了 Inspector 的可访问性，以及检查可访问性（ 🎬 #202 和 🎬 #416）

## 其他话题

 - iPad 上会有一个 Playground App
 - 新的苹果文件系统（APFS）
 - iOS 10 开始用户能够删除苹果的内置应用（股票应用，等等）
 - 苹果开源了加密算法库和 CLI [LZFSE](https://github.com/lzfse/lzfse)

## 各种重要的信息

 - 到 2016 年末，苹果会强制要求所有应用使用 ATS。
 - 现在你 **必须** 在 `Info.plist` 里声明 `XXXUsageDescription`，来获取保护的数据（例如：`NSCalendarUsageDescription`），如果你不这么做，你的应用在获取数据的时候会自动退出！
 
## 链接

为了创建上述清单，我大多数的灵感来源于 Twitter，当然还来自以下文章：

 - [iOS 10 API 的不同点](https://developer.apple.com/library/prerelease/content/releasenotes/General/iOS10APIDiffs/)
 - [“iOS 10 更新说明”](https://developer.apple.com/library/prerelease/content/releasenotes/General/WhatsNewIniOS/Articles/iOS10.html)
> 本文由 SwiftGG 翻译组翻译，已经获得作者翻译授权，最新文章请访问 [http://swift.gg](http://swift.gg)。