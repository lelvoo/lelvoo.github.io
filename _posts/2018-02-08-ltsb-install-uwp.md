---
layout:     post
title:      Windows10 LTSB版安装应用商店与UWP
subtitle:   ——折腾笔记
date:       2018-02-08
author:     Pockies
header-img: img/post-bg-011.jpg
catalog: true
tags:
    - Windows
---

LTSB（长期服务版）是目前唯一可以长期稳定使用的Bug10版本。

它没有烦人的小娜，没有没完没了的Bug更新，没有乱七八糟的内置应用，更不会因为一个build的推送而彻底瘫痪。

但相应的，LTSB也没了应用商店和UWP运行环境。

于是打算把它们装回来：

# 前期准备

准备一个与你LTSB版本号和语言相同的普通版Win10镜像（比如我的版本号是1607，x64系统）。

![](https://wx1.sinaimg.cn/large/741f9461gy1fo8gc4gyilj20lo0iogmw.jpg)

打开镜像，进入 `sources` 文件夹，找到 `install.wim` 文件，用压缩软件打开。

进入 `1` 文件夹，在 `Program Files` 文件夹内找到 `WindowsApps` ，将整个 `WindowsApps` 文件夹解压出来。

![](https://wx3.sinaimg.cn/large/741f9461gy1fo8gc9fpvsj20yh0mp45g.jpg)

进入解压好的 `WindowsApps` 文件夹，保留其中用以下名称开头的文件夹，其余删除。

```
Microsoft.Advertising.Xaml......
Microsoft.NET.Native.Framework......
Microsoft.NET.Native.Runtime......
Microsoft.StorePurchaseApp......
Microsoft.VCLibs......
Microsoft.WindowsStore......
```

得到我们需要的应用商店主程序和UWP运行环境，前期准备结束。

![](https://wx1.sinaimg.cn/large/741f9461gy1fo8gce8xt4j20ur0jdwjt.jpg)

# 权限设置

进入 `C:\Program Files` ，在 `WindowsApps` 文件夹 右键→属性→安全→高级，点击“所有者”后面的“更改”。

在弹出窗口的“对象名称”白框内输入你的用户名（比如我的用户名是pockies），点击“检查名称”自动补全对象名称，随后一路确定直到属性窗口关闭。

![](https://wx2.sinaimg.cn/large/741f9461gy1fo8gcmj57aj20pp0jhdi9.jpg)

双击 `WindowsApps` 文件夹，弹出权限提示，点“继续”获得权限，进入 `WindowsApps` 文件夹，把前期准备提取出来的所有文件放进去。

（如果获取权限失败则回到高级安全设置，手动将你登入的账户权限修改为完全控制。）

![](https://wx4.sinaimg.cn/large/741f9461gy1fo8gcprsopj20am054q35.jpg)

![](https://wx2.sinaimg.cn/large/741f9461gy1fo8gcu4w06j20t80ihgnl.jpg)

再次右键属性进入 `WindowsApps` 的高级安全设置，修改所有者为 `NT Service\TrustedInstaller`，检查名称→确定。

![](https://wx1.sinaimg.cn/large/741f9461gy1fo8gd0baq5j20pp0jh76f.jpg)

回到高级安全设置，点击左下角的 添加→选择主体，输入 `All Application Packages` ，检查名称→确定。

![](https://wx2.sinaimg.cn/large/741f9461gy1fo8gd2ygcaj20qz0kadia.jpg)

相关权限保持默认，确定。

![](https://wx1.sinaimg.cn/large/741f9461gy1fo8gd5hc13j20uk0m4jsq.jpg)

回到高级安全设置，勾选底部的“使用可以从此对象继承的......”。

随后一路应用/确定即可，权限设置结束。

![](https://wx3.sinaimg.cn/large/741f9461gy1fo8gdexzrkj20pp0jhq65.jpg)

# 安装商店

以管理员运行PowerShell，输入以下命令，回车。

```
Add-AppXPackage -Register 'C:\Program Files\WindowsApps\*\AppXManifest.xml' -DisableDevelopmentMode
```

会出现大量红字报错，无视，反复运行该命令直到不再报错即可。

![](https://wx1.sinaimg.cn/large/741f9461gy1fo8gdmujhoj20ld0ifgmx.jpg)

然后你就拥有了可以从Microsoft Store完美安装/运行/更新UWP应用的LTSB版Win10。

该怎么爽随你喜好，个人给黄油板子配置之后运行稳定，续航也好了不少。

![](https://wx3.sinaimg.cn/large/741f9461gy1fo8gdsot18j20y80qs4fj.jpg)
