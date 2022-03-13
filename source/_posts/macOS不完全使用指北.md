---
title: macOS不完全使用指北
date: 2022-03-13 12:13:05
tags: 随笔
categories: 女朋友教程
---

## 0x00 macOS简介
macOS（2011年及之前称 Mac OS X，2012年至2015年称 OS X）是苹果公司推出的基于图形用户界面操作系统，为麦金塔（Macintosh，简称 Mac）系列电脑的主操作系统。
Q: Unix, Linux和MacOS之间有什么联系? 又有什么区别?
A: Linux是类Unix的操作系统, 其内核上的大部分软件是按照POSIX协议运行,所以跟Unix系统上运行效果类似.
MacOS的内核是在Unix的家族分支上的,其内核是基于NeXTSTEP和FreeBSD混合开发组成,所以有部分功能运行的跟Unix系统一样,有部分又不同(定制开发)。
而Linux是一众类Unix操作系统的统称，常见的发行版有ubuntu,Debian,redhat等。
总的来说，macOS拥有和linux相似的文件管理及进程管理机制。
Q: MacOS相对于windows优势在哪里？
A: 优势在于它是类Unix系统。
Q: 我要不要在mac上装windows？
A: 不要。
Q: 如果我一定要装windows怎么办？
A: 那就使用虚拟机来安装，轻度使用windows。

<!--more-->
## 0x01 macOS常用快捷键
Mac中主要有四个修饰键，分别是Command，Control，Option和Shift。
Command键可以理解成类似windows的win键。
通用：
Command + Z 撤销
Command + X 剪切
Command + C 拷贝（Copy）
Command + V 粘贴
Command + A 全选（All）
Command + S 保存（Save)
Command + F 查找（Find）
截图：
Command + Shift + 3 截取全部屏幕到文件
Command + Shift + Control + 3 截取全部屏幕到剪贴板
Command + Shift + 4 截取所选屏幕区域到一个文件，或按空格键仅捕捉一个窗口
Command + Shift + Control + 4 截取所选屏幕区域到剪贴板，或按空格键仅捕捉一个窗口
文件处理：
Command + Shift + N 新建文件夹（New）
Command + Shift + G 调出窗口，可输入绝对路径直达文件夹（Go）
return 这个其实不算快捷键，点击文件，按下可重命名文件
Command + O 打开所选项。在Mac里打开文件不像Windows里直接按Enter
Command + Option + V 作用相当于Windows里的文件剪切。
在其它位置上对文件复制（Command-C），在目的位置按下这个快捷键，文件将被剪切到此位置
Command + ↑ 打开包含当前文件夹的文件夹，相当于Windows里的“向上”
Command + Delete 将文件移至废纸篓
Command + Shift + Delete 清倒废纸篓
Space 快速查看选中的文件，也就是预览功能
切换：
Command + Tab 在应用程序间切换
Command + Shift + Tab 在应用程序间切换（反向）
Command + ~ 在各应用中的窗口间切换
最常用快捷键：
Command + Q 退出当前应用
Command + H 隐藏当前窗口
Command + M 最小化当前窗口
Command + W 关闭当前窗口

单指滑动 = 移动光标
二指滑动 = 滑动滚动条
三指左右滑动 = 切换全屏应用



## 0x02 你应当知道的一些MacOS常识
1.Finder，苹果译作访达，我们可以理解为windows的资源管理器。
2.你不仅可以在App Store中下载软件，也可以在一些第三方网站中下载一些应用。
3.虚拟机就是你的mac把你的cpu、内存分一部分资源出来，虚拟出的一台新的机器，常用的虚拟机软件有vmware等。虚拟机与你真实的机器其实没有本质区别。
4.你其实不需要关机。

## 0x03 你需要了解的一些简单的命令行
由于在类unix系统中，一切皆文件，了解一些简单的命令行更有助于你方便的使用操作系统。
打开终端(Terminal)，看到这个黑黑的小窗口，你就可以使用它与你的Mac进行交互了。
PS：如果想重度使用，建议使用iterm2对命令行交互窗口进行自定义改造。

关于路径
路径有两种，分为绝对路径与相对路径
绝对路径：完整描述一个文件的位置，总是以斜杠 / 开头。例如 /Users/APLanckFish/Movies。
相对路径：是指相对于当前的目录的文件位置，例如你在文件夹/program中，有文件a.mp4，那么文件a.mp4相对于program这个文件夹的路径就是./a.mp4。其中.表示当前路径，..表示上级路径。

pwd 返回命令行当前路径
cd 进入到某个目录(例如cd ..就是返回上级目录, cd /Users/APLanckFish/Movies 就是访问到这个Movies文件夹下)
ls 列出当前目录下的文件
open 用Finder打开某个路径
cp 复制(cp ./a ./b 将本目录的a文件复制一份 命名为b)
rm 删除(rm ./a)
mv 移动(mv ./a ../a 将本目录的文件a移动至上级目录)

## 0x04 进程管理
使用命令行进行进程管理比较复杂，暂时不多介绍。如果你的进程失去了相应，打开工具>活动监视器，直接结束进程就好。