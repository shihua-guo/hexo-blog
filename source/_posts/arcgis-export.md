---
title: arcgis导出
date: 2018-06-27 19:32:07
tags:
---
# arcgis导出

> 基于arcgis javascript api 3.24


最近需要做一个地图导出的需求。有大概一下2个要求：
1.需要导出全市范围（也就是包括视野范围之外的也需要导出）
2.所见即所得，当前页面看到的和导出的一致。
于是，我大致思路如下：
1.使用arcgis自带的PrintTask工具
2.直接将整个地图“截图”下来，保存成图片再给客户。
### 使用PrintTask
使用PrintTask比较简单，管网也有例子。主要步骤如下：
1.new PrintTask(url);这里的url放的是这个工具的服务地址。arcgis官网的是：http://sampleserver6.arcgisonline.com/arcgis/rest/services/Utilities/PrintingTools/GPServer/Export%20Web%20Map%20Task
如果本地有arcserver，那么可以到arcgisserver 后台管理查看
![后台管理查看](/img/arcgis-export/1.png)