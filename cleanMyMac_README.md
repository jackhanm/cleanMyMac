# cleanMyMac
让定时任务为自己的mac清理多余的缓存吧



## 0.建立定时任务清理空间

mac 的macOS是unix衍生的系统，同样支持crontab设置定时任务。

```shell
# 1. 清除Xcode 编译缓存。// 每周二早上9.30执行清理并提醒（作为iOS开发者，每周清理比较有必要）
30 9 * * 2 rm -rf ~/Library/Developer/Xcode/DerivedData/*
30 9 * * 2 osascript -e 'display notification "😄 正在清除Xcode编译缓存..." with title "来自远方的通知" subtitle "from samingzhong" sound name "Blow"'   

# 2. 打开Xcode 设备版本支持相关文件夹。 每3个月早上14.30执行清理并提醒（按需清除）
30 14 * */3 * open ~/Library/Developer/Xcode/iOS\ DeviceSupport
30 14 * */3 * osascript -e 'display notification "😄 已经为您打开了这个文件夹，请注意甄别清理... " with title "距离上回清理iOS DeviceSupport文件夹已经有阵子啦" subtitle "from samingzhong" sound name "Tink"'
```



## 1. Mac清理缓存清单说明

### 1. 删除不需要支持真机调试的相关文件

`/Users/samingzhong/Library/Developer/Xcode/iOS DeviceSupport/` 文件夹下，酌情删除部分文件夹。

就是Xcode支持 Xcode为了能够支持各种各样iOS版本真机调试，在你的设备连接Xcode的时候，Xcode就会把真机上 `/System/Libray/` 文件夹下支持调试相关的文件拷贝到 `/Users/samingzhong/Library/Developer/Xcode/iOS DeviceSupport/9.1 (13B143)/Symbols/System` ,

#### 1.1 文件构成

其中每一个文件夹里有一个 `Symbols`（符号）文件夹，该文件夹下又有`System` , `usr` 文件夹。

##### 1）`System/` 

里边只有一个 `Library` 文件夹，该文件夹下有主要有 `Caches`, `PrivateFrameworks`, `Frameworks` 等文件夹。

###### 1.1) `Caches/`

主要是 `com.apple.dyld` 文件夹，里边包含 `dyld_shared_cache_arm64`, `dyld_shared_cache_armv7s` 文件。

至于这两个文件干嘛用的呢，以下是我找到的一些链接：

> http://iphonedevwiki.net/index.php/Dyld_shared_cache
>
> 

###### 1.2) `PrivateFrameworks/`

###### 1.3) `Frameworks/`

##### 2）`usr/` 

#### 2. 删除项目编译缓存

/Users/samingzhong/Library/Developer/Xcode/DerivedData

每个项目与编译相关的缓存文件，比如说预编译的文件、某个架构的编译缓存。





### 