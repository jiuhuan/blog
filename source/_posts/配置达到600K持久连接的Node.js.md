---
title: 配置达到600K持久连接的Node.js
date: 2016-03-30 10:52:40
tags: 
- Node.js
categories: 
- javascript
---

设置以下参数启动你的Node.js应用程序：
```base
node --nouse-idle-notification --expose-gc --max-new-space-size=2048 --max-old-space-size=8192 ./server/websocketserver.js
```


### –nouse-idle-notification

打开空闲垃圾回收这样会让GC不断运行，是毁灭性的实时服务器环境。如果不关闭系统将获得将近每秒一次每隔几秒钟长hickup。

### –expose-gc

使用手动操作-GC命令。

### –max-old-space-size=8192 (单位为 MB)

增加了每个node进程的最大使用内存8Gb，而不是在64位机器上默认的1.4Gb。

### –max-new-space-size=2048 (单位为 KB)

为了减少 Full GC 的停顿，可以限制 new space 的大小为 2Mb.

如果不使用这个参数停顿有点长，但机器会处理好一点。在这种情况下你需要什么取决于项目需求。
