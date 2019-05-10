---
layout:     post
title:      在Windows下利用WoL实现多台电脑“联动”开机
subtitle:   折腾笔记
date:       2019-05-10
author:     Pockies
header-img: img/post-bg-011.jpg
catalog: true
tags:
    - Windows
---

人总会有些奇葩需求。

比如不是每个人都愿意让NAS/服务器 7*24小时工作，更多时候他们只需要在标准工作时间内访问服务端内容。

解决方案多种多样，比如：

- 服务端设置计划任务定时休眠/唤醒；
- 路由器设置计划任务定时WoL。

但最优解无疑是：

- **客户端“电脑A”启动时，服务端“电脑B”也跟着自动开机。**

**绝不白给一丝电费。**

于是就开始了折腾。

# 启用网络唤醒（WoL）

[网络唤醒](https://zh.wikipedia.org/wiki/%E7%B6%B2%E8%B7%AF%E5%96%9A%E9%86%92)`（WoL/Wake-on-LAN）`是绝大多数主板都会自带的功能。

强大，便利，异常实用，不花一分钱，诸如“远程开机”“手机遥控开机”等一系列骚操作都离不开WoL。

哪怕你暂时用不上，也强烈推荐开启。

**因为这是迟早会用，且用过一次就再也回不去的功能。**

#### 配置BIOS

既然是集成在主板上的，第一步自然得进BIOS启用这项功能。

相关设置一般包含“PME” / “Wake on Lan” / “WoL”等字眼，如果找不到，请阅读主板说明书或者直接Google。

例如我这块垃圾主板藏在“高级电源管理”里，名字叫做“PME唤醒”。

![](https://raw.githubusercontent.com/Pockies/pic/master/741f9461ly1g2wassl4eij21400mm4m0.jpg)

#### 配置网卡驱动

`Win+R` 打开“运行”，输入 `devmgmt.msc`，“确定”以打开“设备管理器”：

![](https://raw.githubusercontent.com/Pockies/pic/master/%E8%BF%90%E8%A1%8C(473).png)

展开“设备管理器”的“网络适配器”，找到网卡驱动，右键“属性”。

在“高级”里将“魔术封包唤醒”与“关机 网络唤醒”设置为开启：

![](https://raw.githubusercontent.com/Pockies/pic/master/Realtek%20PCIe%20GBE%20Family%20Controller%20%E5%B1%9E%E6%80%A7(471).png)

同时在“电源管理”里勾选“允许此设备唤醒计算机”：

![](https://raw.githubusercontent.com/Pockies/pic/master/Realtek%20PCIe%20GBE%20Family%20Controller%20%E5%B1%9E%E6%80%A7(475).png)

网络唤醒启用完毕。

这时给手机装个[Wake On Lan](https://play.google.com/store/apps/details?id=co.uk.mrwebb.wakeonlan)之类的App，扫描并添加你已经开启WoL的PC，只需掏出手机轻轻一点，就能在局域网内**遥控开机**了。

![](https://raw.githubusercontent.com/Pockies/pic/master/Screenshot_20190510-171940.png)

# 配置“联动”开机

原本还在傻缺的折腾计划任务，结果发现有更简单粗暴的姿势：

#### 给“电脑A”安装WOL.EXE

与上文提到的手机App[Wake On Lan](https://play.google.com/store/apps/details?id=co.uk.mrwebb.wakeonlan)一样，[WOL.EXE](https://www.gammadyne.com/cmdline.htm#wol)也是一款网络唤醒软件，不过它完全基于命令行。

其内容物只有一个193kb的“wol.exe”，**直接把它扔到**`C:\Windows`**里便完成了“安装”。**

要是不嫌麻烦，也可以自定义“安装”位置：

`Win+Pause`打开“系统属性”，进入“高级系统设置”。

![](https://raw.githubusercontent.com/Pockies/pic/master/%E7%B3%BB%E7%BB%9F(479).png)

点击“环境变量”，选中“系统变量”里的“Path”并“编辑”，在弹出对话框里点击“新建”，填入存放“wol.exe”的目录即可。（右键查看大图）

![](https://raw.githubusercontent.com/Pockies/pic/master/%E7%BC%96%E8%BE%91%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F(480).png)

例如我放在了`C:\Software\Internet\wol`。

这时你也差不多看明白了，为什么把“wol.exe”直接扔进`C:\Windows`同样等于安装完毕，因为`C:\Windows`已经默认存在于Path里。

打开CMD，输入wol，返回wol.exe版本信息，安装成功。

![](https://raw.githubusercontent.com/Pockies/pic/master/Administrator_%20%E5%91%BD%E4%BB%A4%E6%8F%90%E7%A4%BA%E7%AC%A6(481).png)

#### 获取“电脑B”的MAC地址

WOL.EXE的命令很简单，cmd输入`wol 目标电脑的mac地址`即可网络唤醒。

引用官网示例：

```
wol 5c9d32b5f287
wol 5c-9d-32-b5-f2-87 192.168.0.1
wol 5C:9D:32:B5:F2:87 192.168.0.1 16962
wol 5C.9D.32.B5.F2.87 9
以上四种命令姿势皆可
```

于是我们**至少需要**搞到“电脑B”的mac地址：

在已启用网络唤醒的“电脑B”上打开CMD，输入`ipconfig /all`，返回内容里的`Physical Address/物理地址`就是mac地址了。

![](https://raw.githubusercontent.com/Pockies/pic/master/Administrator_%20%E5%91%BD%E4%BB%A4%E6%8F%90%E7%A4%BA%E7%AC%A6(477).png)

记下即可。

#### 简单的写个批处理

我们已经给“电脑A”装上了wol.exe，也拿到了“电脑B”的mac地址；

意味着现在只需在“电脑A”上输入一条命令，便能网络唤醒“电脑B”

**——然而总不能每次都手输命令不是？**

在“电脑A”上新建一个文本文档，填入以下内容：

```
@echo off
wol 电脑B的mac地址
```

例如：

```
@echo off
wol 5c-9d-32-b5-f2-87
```

保存并将文本文档重命名为`wol.bat`。

只需双击运行这个批处理就能启动“电脑B”了。

#### 优雅的写个启动脚本

要知道我们的最终目标可是：

- 客户端**“电脑A”**启动时，服务端**“电脑B”**跟着自动开机。

**——结果现在每次都得双击运行一次批处理，批处理还会闪个弹窗，多麻烦！**

让我们继续在“电脑A”上新建一个文本文档，填入以下内容：

```
Set ws = CreateObject("Wscript.Shell") 
   ws.run "cmd /c wol.bat的存放位置",vbhide
```

例如：

```
Set ws = CreateObject("Wscript.Shell") 
   ws.run "cmd /c C:\Software\Internet\wol\wol.bat",vbhide
```

保存并将文本文档重命名为`wol.vbs`。

然后将它移动到`C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp`：

![](https://raw.githubusercontent.com/Pockies/pic/master/%E5%90%AF%E5%8A%A8(482).png)

每次“电脑A”开机都会启动这个脚本，脚本又会在**不弹出任何窗口的情况下**自动运行批处理，“电脑B”也就跟着自动开机了。

至此，我们已经优雅的实现了“联动开机”。

# 尾巴

本想着顺便配置一下“联动关机”。

在“电脑B”上打开“组策略编辑器”，按图找到“从远端系统强制关机”，双击并添加你的登录用户。

![](https://raw.githubusercontent.com/Pockies/pic/master/POCKIES-NAS%20-%20%E8%BF%9C%E7%A8%8B%E6%A1%8C%E9%9D%A2%E8%BF%9E%E6%8E%A5(483).png)

接着在电脑A写个批处理：

```
@echo off
net use \\电脑B的IP\ipc$ "电脑B密码"/user:"电脑B用户名"
shutdown -s -m \\电脑B的IP -t 60
```

双击运行就能远程关机。

**——然而趴在地上想了想**

同步关机反而会引发麻烦，万一电脑A**更新个Bug10之类**需要重启，那电脑B岂不得跟着开关机一轮......

万一在电脑B的开关机过程中，遇到正在访问电脑B内容的其它用户，画面不要太美......

![](https://raw.githubusercontent.com/Pockies/pic/master/(201)2.png)

作罢。

同步开机就够了，关机还是乖乖定时，交给计划任务吧......