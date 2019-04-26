---
layout:     post
title:      从Win10 LTSB 2016升级到LTSC 2019并安装应用商店
subtitle:   折腾笔记
date:       2018-10-05
author:     Pockies
header-img: img/post-bg-011.jpg
catalog: true
tags:
    - Windows
---

本打算LTSB 2016用到微软倒闭，无奈巨硬不给这个机会：

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjaqj6woj20rh0jq0uo.jpg)

越来越多实用的小工具彻底转到了巨硬商店，却加上了版本限制。

想要安装只能升级。

# 升级安装至普通版1809

一时兴起试着玩，结果玩出了迷之bug：

- 升级安装将 **只能保留个人文件，不能保留应用。**

- 升级安装完成后，所有正常软件和商店应用消失，但唯独安装的 **黄色游戏** 一个没少的躺在开始菜单里。

  这就......

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjj8vnlrj20f20f4wo2.jpg)

- 小娜和其他垃圾内置广告功能依然烦人。

- 滚回操作变得繁琐，先是吓唬说回滚丢软件掉文档（实际不会），回滚前至少弹出三个以上窗口让你选择，并且反复恶意调换“下一步”按钮位置诱导人误操作，深得国产流氓软件卸载真传。

  好在回滚安全成功，没遇到失败“bug”。

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvvc2adeg0j20k50e10t6.jpg)

# 升级安装至LTSC 2019

还是装着玩，用的 **升级安装** ，整个升级流程相当惊喜（褒义）。

个人非常推荐直接保留文件+应用升级安装（升级前请先卸载onedrive）。

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvw9xmx1kxj20kc0gawfl.jpg)

- 和普通1809不同，升级安装至LTSC 2019居然真能 **完整保留个人文件和应用** ，且没什么bug。 

- 如果你的LTSB 2016手动安装过应用商店和uwp环境，**升级安装将同样完整保留并正常运行**，包括你安装的商店应用。

- 整个过程顺畅得不像bug10，所有东西全部保留，完全不像跨版本更新，更像是打了一个例行小补丁。

- **LTSB 2016的数字激活无法用于LTSC 2019，请重新激活。**

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvwaoc1ut5j20js08t0u0.jpg)

- bug只发现了一个：onedrive的资源管理器快捷方式点击会无反应，反复卸载安装无解。

  **所以升级安装，请先卸载onedrive。**

# 全新安装至LTSC 2019 & 安装应用商店

由于OneDrive的小bug逼死强迫症，于是干脆全新安装了。

**应用商店和uwp环境的安装方法不变**，请移步： 

[Windows10 LTSB/LTSC版安装应用商店与UWP](https://pockies.github.io/2018/02/08/ltsb-install-uwp/)

值得一提的是，全新安装完整暴露出LTSC的自带软件情况后，发现这个版本并不算“干净”：

- 不自带“游戏工具栏”（ `Win+G` 唤醒的那玩意），但windows设置里却硬塞了一个入口。

  如果你没有手动安装应用商店，并通过商店把“游戏工具栏”重新装上，那这个入口就死活摆在这里，你无法隐藏，还用不了。

  **逼死强迫症。**

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjapaxbfj20dk08pdg3.jpg)

- 不自带“截图和草图”（1809里用来替代旧版“截图”的uwp应用），通知和操作里又给你塞了个入口。

  并且点击真能截图， **但是不能保存** ，除非你又通过商店把“截图和草图”给装上。

  **强迫症又死了。**

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjaobds1j20gr0aygmj.jpg)

- 不自带“人脉”，但任务栏又又又给你留了个入口。

  于是老样子，不通过商店重新安装“人脉”或者干脆隐藏，那这玩意就又摆在这里让你看着玩了。

  **强迫症想刨了阿三祖坟。**

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjj3b6bgj20ah0iy784.jpg)

- 接着是本次1809的“重磅功能”之一：剪贴板历史

  `Win+V` 体验极差，由于内容卡片太大而窗口太小，导致显示的项目极少，还不能拉大窗口或全屏，使用下来极其低效。

  并且一天不到已经出现了 `Win+V` 无法唤出的抽风问题。

  最后安心用回chrome扩展，瞬间爽到：[Clipboard History 2](https://chrome.google.com/webstore/detail/clipboard-history-2/ajiejmhbejpdgkkigpddefnjmgcbkenk)

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjj37ph3j209e0dgjsr.jpg)

- 然后是本次1809的“重磅功能”之二：剪贴板同步

  ![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjalfl2oj20ef0gytad.jpg)

  是的，直到最后我都没能体验到这功能，因为...

  第一次点击上图红框的弹窗如图：

  ![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjj3a6l2j20ic0bmdh3.jpg)

  play上发现有个同名输入法但开发者并不是巨硬。

  毕竟是内容敏感的剪贴板，安全起见我填了手机，收到一条短信并打开google play安装应用，结果发现还真tnd是这 [输入法](https://play.google.com/store/apps/details?id=com.touchtype.swiftkey.beta&hl=ja)。

  期间由于半天没等到短信，我又点了一次，弹窗如图：

  ![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjahvqgmj20j00ihjsq.jpg)

  突然就变样了，同样填入手机收到的却是一条coolapk的网页短链，让你安装巨硬的[launcher](https://www.coolapk.com/apk/com.microsoft.launcher)。

  ![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjodtmpmj20i20hb16n.jpg)

  输入法变launcher，安装的提供者从play变成coolapk，不确定是不是bug，或者跟代理/位置区域设置有关。

  我选择告辞，毕竟剪贴板内容敏感。

  也不可能为了区区一个“剪贴板跨平台同步”而抛弃Gboard和Nova launcher转投这些废品。

  **毕竟这功能有的是优秀又轻量的替代**，比如： [Snapcopy](http://snapcopyapp.com/) 。

- 最后是本次1809的“重磅功能”之三：活动历史记录。

  不能记录开启过哪些程序，也就没什么意义。

  如果开启这功能，还会在历史记录的最底部提示让你向巨硬发送活动记录，你只能选“是”，要么那提示就一直在那烦人。

  索性整个关了一了百了，关闭选项藏在设置的“隐私”里。

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjabljvrj20po0mkdm9.jpg)

# 尾巴

实际这次1809/LTSC 2019也是有不错的改进。

个人最喜欢的是夜间模式，开始菜单能拖拽建立文件夹，以及chrome能右键快速调用一个Emoji输入板。

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461gy1fvxjj37ttmj20ab0af75d.jpg)

我也终于能正常安装商店内那些有版本要求的小软件了。

除此之外，就剩一堆逼死强迫症的残留入口，不怎么稳定的设置（容易闪退），以及一卡一卡还不完整的Flunet Design特效。

最失望的莫过于Sets没有实装，连带着窗口的Flunet Design模糊特效一并咕咕。

板子和nas我就不升级了。

**LTSB 2016用到地球重启！！**