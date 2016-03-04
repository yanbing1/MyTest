# iOS沙盒路径分析222
### 目录
---
* [沙盒目录的构成](#沙盒目录的构成)
* [应用程序包](#应用程序包)
* [Documents目录介绍](#Documents目录介绍)
* [Library目录介绍](#Library目录介绍)
* [tmp目录介绍](#tmp目录介绍)


### 沙盒目录的构成
---
每个应用程序都在自己的沙盒内，不能随意跨越自己的沙盒去访问别的应用程序沙盒的内容，应用程序向外请求或者接收数据都需要经过权限认证。虽然沙盒中有这么多文件夹，但是没有文件夹都不尽相同，都有各自的特性。所以在选择存放目录时，一定要认真选择适合的目录。
沙盒目录由以下四部分构成：应用程序包、Documents、Library、tmp。下面我们来看一下这些文件目录的作用

### 应用程序包
---
"应用程序包": 这里面存放的是应用程序的源文件，包括资源文件和可执行文件。

let path = NSBundle.mainBundle().bundlePath

### Documents目录介绍
---
Documents 为最常用的目录，iTunes同步该应用时会同步此文件夹中的内容，适合存储重要数据。

let documentPaths = NSSearchPathForDirectoriesInDomains(NSSearchPathDirectory.DocumentDirectory, NSSearchPathDomainMask.UserDomainMask, true)let documentPath = documentPaths[0] as! String或者let documentPath = NSHomeDirectory() + "/Documents"

### Library目录介绍
---
Library目录下面有两个目录构成:Cache和Preterences

Library/Caches: iTunes不会同步此文件夹，适合存储体积大，不需要备份的非重要数据。

let cachePaths = NSSearchPathForDirectoriesInDomains(NSSearchPathDirectory.CachesDirectory, NSSearchPathDomainMask.UserDomainMask, true)let CachePath = cachePaths[0] as! String或者let documentPath = NSHomeDirectory() + "/Library"let documentPath = NSHomeDirectory() + "/Library/Caches"

Library/Preferences: iTunes同步该应用时会同步此文件夹中的内容，通常保存应用的设置信息。

### tmp目录介绍
---
tmp: iTunes不会同步此文件夹，系统可能在应用没运行时就删除该目录下的文件，所以此目录适合保存应用中的一些临时文件，用完就删除。

let tmpPath = NSTemporaryDirectory()