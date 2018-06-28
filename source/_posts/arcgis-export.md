---
title: arcgis导出
date: 2018-06-27 19:32:07
tags:
---
# arcgis导出

> 基于arcgis javascript api 3.24

### 背景
最近需要做一个地图导出的需求。有大概一下2个要求：
1. 需要导出全市范围（也就是包括视野范围之外的也需要导出）
2. 所见即所得，当前页面看到的和导出的一致。

于是，我大致思路如下：
1. 使用arcgis自带的PrintTask工具
2. 直接将整个地图“截图”下来，保存成图片再给客户。

### 使用PrintTask
使用PrintTask比较简单，官网也有例子。主要步骤如下：
1. var printTask = new PrintTask(url);
  > 这里的url放的是这个工具的服务地址。arcgis官网的是：http://sampleserver6.arcgisonline.com/arcgis/rest/services/Utilities/PrintingTools/GPServer/Export%20Web%20Map%20Task
  如果本地有arcserver，那么本地的地址可以到arcgisserver 后台管理查看,进入后台管理后，点击左边的 **Utilities** 然后看到 **PrintingTools** 就是了。

  ![后台管理查看](/img/arcgis-export/1.png)

1. var params = new PrintParameters();建立导出的模板PrintParameters，具体参数去api查看。并且设置map： params.map = map;

2. 执行：printTask.execute(params, printResult=>{});这里会回调一个printResult，里面带有图片或者pdf等文件的下载地址。
  > 注意：导出可能会遇到超时问题。

但是呢，我遇到了以下问题：
1. 最严重的是，导出速度非常非常非常慢。经测试，最简单的导出需要3分钟左右。所以会遇到超时问题，这里需要设置一下esriConfig。代码如下：
  ```javascript
  import esriConfig = require("esri/config")
  ...
  esriConfig.defaults.io.timeout = 300000;//这里设置你的超时时间
  ```
  > 开始我以为是来源于PrintingTools服务的 **客户端可使用服务的最长时间** 设置造成的，其实并不是。是因为esri默认的请求时间是1分钟。

2. 导出的分辨率低，而且不能识别某些图层。比如我使用featureSet构建的图层。

以上，PrintingTools导出的速度基本就判死刑了。经我们公司的arcgis人员使用arcserver导出也是非常慢。原因不得而知，cpu/内存占用几乎没变化，并且导出会提示内存不足，但是内存十分充足。
>所以在这里请教一下大家，是因为gpu的问题吗？服务器并没有显卡。所以，我今天选择了第二种方法：截图。


### 截图保存
  > 有了这个想法，我就查了，并且查到相关的：[arcgis api for js入门开发系列二十打印地图的那些事](https://www.jianshu.com/p/e7b82caa12b5)。非常感谢！

