---
title: parceljs2与webpack5性能对比
date: 2021-5-26 14:16:35
tags: [技术文档]
categories: 开发心得
layout: post
---
## parceljs2与webpack5对比文档

1. 根据实际测试情况，在只初始化安装React,ReactDom,Typescript,babel等必要插件等情况下，两种方案的性能优劣表现如下

| 方案     | 开发编译时间（不含缓存） | 打包时间（不含缓存） |
| -------- | ------------------------ | -------------------- |
| parceljs | 1.83s                    | 2.99s                |
| webpack  | 2.08s                    | 3.42s                |
<!--more-->
parcel的编译耗时：

![parcel_dev](/images/parcel2webpack5/parcel_dev.png)

parcel的打包耗时：

![parcel_build](/images/parcel2webpack5/parcel_build.png)

webpack的编译耗时:

![webpack_dev](/images/parcel2webpack5/webpack_dev.png)

webpack的打包耗时:

![webpack_build](/images/parcel2webpack5/webpack_build.png)

双方的依赖项对比：

Webpack:

![webpack_dep](/images/parcel2webpack5/webpack_dep.png)

parcel:

![parcel_dep](/images/parcel2webpack5/parcel_dep.png)

结论1:在空项目下，parceljs2的性能略好于webpack5.

-------------------------

2. 关于多页应用打包等其他项功能对比

   | 方案     | 是否支持多页面打包 | 配置上手难易度 | 兼容性 | tree-shaking | dynamic import |
   | -------- | ------------------ | -------------- | ------ | ------------ | -------------- |
   | parceljs | 是                 | 较小           | 略好   | 实验性支持   | 支持           |
   | webpack  | 是                 | 较大           | 好     | 支持         | 支持           |

   结论2:

   parcel与webpack都支持多页面打包，webpack在entry中指定多个入口文件就可以，parcel build 也可以使用通配符等来指定多个目标文件。

   parcel推崇0配置的理念，但在实践中通常还是使用配置文件来加载命令，配置项也较少，而webpack的配置项非常多也很繁琐，配置上手难易度webpack显著高于parcel。

   兼容性方面webpack是最主流的编译工具，基本能覆盖绝大多数使用场景。

   parcel与webpack都支持tree-shaking，parcel默认为禁止，可使用--experimental-scope-hoisting打开实验性的tree-shaking支持，但可能不稳定，后续可能有其他坑。webpack可使用sideEffects属性来支持tree-shaking。

   parcel与webpack都支持动态导入模块。

--------------------

综合结论:

webpack5更加符合我们的使用场景。虽然webpack使用更加复杂，但这是一个比较成熟稳定的方案，已知的坑比较少，相关技术讨论也比较多。而且在项目文件较多的情况下也未必能保证parceljs性能依然能保持优势，因此保守方案是最佳选择。