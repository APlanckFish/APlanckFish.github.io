---
title: Aria2破解百度网盘
date: 202-12-01 19:59:32
tags: [开发工具]
categories: 开发工具
---

## 百度网盘破解攻略

众所周知，由于百度的限制，非会员下载速度只有不到100KB/s。

aria2作为下载神器，配合油猴脚本可以比较轻松的绕过对百度网盘的限制。



话不多说，直接上链接：

-----

### 油猴脚本

[官方插件地址](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=zh-CN)需翻墙。

一些好用的解析百度直链的脚本插件

1. [秒传链接提取](https://greasyfork.org/zh-CN/scripts/424574-%E7%A7%92%E4%BC%A0%E9%93%BE%E6%8E%A5%E6%8F%90%E5%8F%96)

2. [百度网盘简易下载助手(直链下载复活版)](https://greasyfork.org/zh-CN/scripts/418182-%E7%99%BE%E5%BA%A6%E7%BD%91%E7%9B%98%E7%AE%80%E6%98%93%E4%B8%8B%E8%BD%BD%E5%8A%A9%E6%89%8B-%E7%9B%B4%E9%93%BE%E4%B8%8B%E8%BD%BD%E5%A4%8D%E6%B4%BB%E7%89%88)
3. ~~[百度导出助手](https://github.com/acgotaku/BaiduExporter)作为最早以及最广泛传播的插件，由于众所周知的原因，该插件已下架~~
4. [极下解析](https://jixia.baidui.vip/#/login)该网站也提供解析直链服务。

以上插件任选其一安装即可。本人使用的是第二个。

__Attention:油猴脚本若无法安装，记得打开chrome的开发者模式，然后将crx文件拖入进去__。

__百度云每日限制下载量在10G左右，后续还是会掉下来，太频繁可能会被百度拉入黑名单，慎重使用。__

------

### Aira2

大名鼎鼎的下载工具就不过多介绍了,[官方地址在这里](https://github.com/aria2/aria2)。

如果你是Mac用户，直接

```bash
brew install aria2
```

windows用户可寻找对应安装包

-----

### 使用方式

1. 下载aria2的[webGUI](http://43.154.154.63:8080/aria2-web.html)到本地。

2. mac打开aria2的服务,执行

   ```aria2c```

   ![image-20221201180440192](/Users/chenpanbo/program/APlanckFish.github.io/source/images/image-20221201180440192.png)

出现以下字样则成功启动。

3. 打开[百度云网站](https://yun.baidu.com)，根据对应的脚本提示将资源导出到aria2，然后你就能得到飞快的下载速度了。

4. 下载结束，在终端使用control + c 关闭aria2服务。

----

感谢各位大神的工具搭建，尤其是pandownload的作者。

__Fuck Baidu__

