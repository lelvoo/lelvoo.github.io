---

layout:     post
title:      利用PicGo快速迁移Weibo外链图片到GitHub
subtitle:   昨天，Weibo开始屏蔽图片外链了。
date:       2019-04-27
author:     Pockies
header-img: img/post-bg-011.jpg
catalog: true
tags:
    - 生活
---

直到昨天上午，Weibo都是地球上最好用的图床。

- 完全免费，秒速访问，极其稳定，不限流量，永久保存。
- 除了会压图与审查色情/敏感内容，简直无可挑剔。

正因如此，包括我在内将Weibo当作主力“图床”的人不在少数，连相关[Chrome扩展](https://chrome.google.com/webstore/search/%E5%BE%AE%E5%8D%9A%20%E5%9B%BE%E5%BA%8A?utm_source=chrome-ntp-icon&_category=extensions)都有好几个。

然而——

> 天下没有免费的午餐。

就在昨天早上，Weibo毫无通告的开启了防盗链，站外引用图片集体403。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies19.04.27-01.40.55.png)

我的Blog昨天受灾惨重几乎等于瘫痪，尤其一些长篇图文教程。

虽然被Weibo这轮背刺搞得满肚子窝火，但Weibo在**并没有“图床服务”**的情况下**一直开放外链**让我们爽了7年之久，也算仁至义尽。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-14.15.07.png)

所以面对~~辣鸡~~可乐的~~无端~~指责，我竟无法反驳，甚至痛定思痛点了个赞......

不过图床boom了，总得想办法。

**本文将介绍一些迁移方案，也强烈建议使用weibo做图床的朋友尽快迁移。**

# 利用GitHub当免费图床

> 没有面包，吃蛋糕不就好了？

反正Blog就是用GitHub搭建，干脆一不做二不休，直接拿GitHub当图床便是：

打开[GitHub](https://github.com)，点右上角新建仓库。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-14.36.50.png)

起一个名字，如`pic` ，设为公开（私密将无法外链显示），点击`Create repository`。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-14.37.17.png)

然后进入网页 [github.com/settings/tokens](https://github.com/settings/tokens)，点击`Generate new token`。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-14.45.32.png)

填写令牌描述，如`pic`；设置里勾选`repo`，拉到网页底部，点击`Generate token` 生成令牌。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-14.50.11.png)

**※务必复制保存这串令牌备用，GitHub只会显示这一次。**

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-14.52.10.png)

GitHub配置结束。

# 使用PicGo传图到GitHub

[PicGo](https://github.com/Molunerfinn/PicGo)是一款支持多图床上传的客户端软件，功能强大。

根据你的系统下载安装对应的[PicGo](https://github.com/Molunerfinn/PicGo/releases)版本，打开软件并展开右侧`图床设置`；

进入[GitHub图床](https://nodejs.org/en/)，在设置里依次填入：

- 仓库名。

  填写`你的GitHub用户名/pic`，也就是上一步建立的GitHub仓库；

- 分支名。

  填写`master`即可；

- Token。

  填写上一步获取的GitHub令牌。

点击`确定`，并`设为默认图床`。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-15.08.07.png)

然后进入PicGo的上传区，拖拽图片即可上传，上传完成会根据底部选择的`链接格式`，自动复制对应格式的文本到剪贴板。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-15.19.42.png)

现在，你已经能拿GitHub当图床使了：

- 不仅能通过[GitHub ](https://desktop.github.com/)网页直接访问图床仓库，简单管理已上传的图片；
- 也可以安装[GitHub Desktop](https://desktop.github.com/)将仓库克隆到本地，在本地管理/修改图片后再推送回去。

**但必须注意，上传大体积图片务必压缩，不然载入速度感人，体积控制在200kb内最佳。**

图片压缩工具推荐使用：

- [imageoptim](https://imageoptim.com/api)；
- [imagine](https://github.com/meowtec/Imagine/releases)；
- [weibo](https://www.weibo.com)。~~传上去再扒下来图片会自动压缩，继续漂weibo服务器。~~

# 批量迁移Weibo外链图片

上文解决了未来的图床需求。

但旧文引用的weibo图片还在集体403，总得抢救一下：

同样打开PicGo，进入右侧`插件设置`，输入`pic-migrater`搜索安装[picgo-plugin-pic-migrater](https://github.com/PicGo/picgo-plugin-pic-migrater)插件。

首次安装该插件会提示安装[Node.js](https://nodejs.org/en/)，同样安装即可。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-15.53.39.png)

安装完成重启软件，点击插件右下角的齿轮图标，`选择文件`。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-15.58.84.png)

在弹出对话框内打开你想转移图片的文章**（必须是Markdown格式）**。

![](https://raw.githubusercontent.com/Pockies/pic/master/%E6%89%93%E5%BC%80(468).png)

软件会自动抓取文内所有Weibo图片，并上传至PicGo的**默认图床**（如上文设置的github），同时自动将文内的Weibo外链替换成新图床。

**——一键批量迁移所有文内图片，且不会改变文章内容，完全无痛。**

迁移完成后会以`旧文件名_new.md`的文件名生成新文章到同目录，确认文章内容无误后替换掉旧文章即可。

**必须注意：**

- 该插件**仅支持Markdown**编写的文章，请将文章或图片链接写成Markdown再使用。

  也推荐借此机会学习一下Markdown，语法非常简单；编写软件推荐[Typora](https://www.typora.io/)，傻瓜易用。

- 插件支持大批量操作，点击`选择文件夹`就能扫描**某文件夹内**的**所有文章**并批量迁移。

  **但不推荐使用该功能**，一旦图片迁移失败，你会搞不清到底是哪篇失败，直接抓瞎，老老实实一篇一篇迁移就好。

- 如果你的单篇文章较长（>3000字），且图片数量不少（>10张），建议将文章**拆分**成几份再迁移。

  **否则同样有概率迁移失败。**

- **时刻关注右下角通知**，出现迁移失败就赶紧检查，一两张失败推荐扒下来手动上传，数量过多就拆分文章重试。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27.01.23.59.png)

- 手动上传偶尔也会失败，**修改一下图片文件名**再传即可。

整个Blog的图床问题至此彻底解决。

# 解决weibo外链图片的403错误

自己的Blog图片是迁移了，但别人的可不一定。

一些引用Weibo图片又来不及迁移的地方（如论坛帖子）照样403，这时我们可以Ban掉refer临时救急。 

安装Chrome扩展如[Referer Control](https://chrome.google.com/webstore/detail/referer-control/hnkcfpcejkafcihlgbojoidoihckciin)，进入扩展设置：

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-17.01.357.png)

- `site filter`内填入`sinaimg.cn`；
- `referer setting`选择`Block`。

之后Weibo的外链图片就会正常显示。

Weibo测试图片（1.3MB，GIF）：

![](https://wx3.sinaimg.cn/large/741f9461ly1g2hgoq61w3g20eg085b29.gif)

# 其它图床推荐

GitHub算是目前**免费图床**里最稳定，且最便利的一个。

然而Weibo昨天才“教育完”我们：

> 鸡蛋不要放在一个篮子里。

所以额外推荐几个当作备胎。

#### OneDrive

没错，就是巨硬的[OneDrive](https://onedrive.live.com/)。

将图片上传OneDrive，右键，选择`嵌入`，网页右侧就会生成链接。

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-18.21.13.png)

普通图片直接引用张贴即可；如果是GIF动图，则需要**删除链接末尾的高宽设置**，如我这张末尾的`?width=520&height=293&cropmode=none`，否则GIF不会动。

OneDrive测试图片（1.3MB，GIF）：

![](https://hsiqlg.bn.files.1drv.com/y4m2IMh7hR7hi8Yh4P1MXlsXIlNB9Zi9lQpPv8ayAlaO1po1bbtnWJP8PQTYxsBn4rgzMtdg7LSIthtk0CtswyEs9SrnargT9xVJcU-hj_i8JW8myD8GUKjMaEfy3hjFNbdkliMCmI4V6pNYaHMWIdFtuH6oJM3uJtqDo0zWkFYyRRtyCKIeepZ_MxHe6n79UfKDOwMUY0SxkEzZzDQFgsppw)

而OneDrive初始容量有15GB，存点Blog图片完全够用。

同时没有流量限制，还能直接像管理网盘那样，分类/移动/重命名自己的图片且不影响已生成的外链，非常方便。

**所以大可将Blog图片备份在OneDrive，顺便获取嵌入链接当作第二图床，一举两得。**

#### SM.MS/Upload.cc

[SM.MS](https://sm.ms/)是码农圈儿里相对知名的一个图床。

因为开放API，上文使用的PicGo甚至直接集成了SM.MS，并将其放在首位。

**服务优秀，目前免费，外链秒开。**

我们~~可爱~~又熟悉但不愿透露姓名的某位还是其团队成员之一。

**缺点也是有的：**

- **存在内容审查。**

  尤其政治敏感内容与色情图片，按内部成员说法，审查方式为AI自动+人工审核，不算宽松。

  ![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-19.03.30.png)

- **因不可抗力暂时撤掉了国内CDN。**

  稳定时外链秒开，拥挤时刷不出图片。由于昨天有相当数量的人数迁移weibo图片到SM.MS，一段时间慢到令人发指，今天也不算乐观。

- **图片一次只能上传10张。**

  想用PicGo批量迁移Weibo图片到SM.MS的可以歇了，一旦文章图片超过10张，多出的图片直接迁移失败。

- **没有历史记录。**

除此之外一切美好。

SM.MS测试图片（1.3MB，GIF，~~目前可能慢到刷不出来，请点击[该外链](https://i.loli.net/2019/04/27/5cc43cdbb583d.gif)直接感受一下...~~）：

![](https://i.loli.net/2019/04/27/5cc43cdbb583d.gif)

---

与SM.MS类似，免费图床还有[Upload.cc](https://upload.cc/)。

**审查相对宽松，服务稳定，并提供一个简单的历史记录。**

Upload.cc测试图片（1.3MB，GIF）：

![](https://upload.cc/i1/2019/04/27/MYKjnx.gif)

**※使用任何图床，务必阅读[使用条款](https://upload.cc/terms)，请勿上传违规内容。**

---

无论[SM.MS](https://sm.ms/)还是[Upload.cc](https://upload.cc/)。

用作论坛帖子之类的**临时**图床都非常合适，但对于**需要长期保存**的重要内容（如Blog图片），请慎重考虑。

**——就像Weibo，免费服务没有义务对用户负责，体量不大的私人图床更可能随时闭门谢客。**

所以本次图床迁移，个人首选用的GitHub，备选用的OneDrive。

哪怕未来巨硬关服务，也不至于瞬间暴毙连个迁移/存档的机会都没有。

# 尾巴 / 致歉

最近Blog除了图床迁移，还有评论插件的修改。

由于我始终都开着[广告屏蔽](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm)，以至于最近才发现[Disqus](https://disqus.com/)居然在评论区硬塞了三处大幅广告，直接影响评论内容的正常展示：

![](https://raw.githubusercontent.com/Pockies/pic/master/Pockies.19.04.27-19.49.37.png)

**神TM我自己都没想过给Blog加广告，你区区一个评论插件居然偷摸开了整整三处，还让人月付10刀才能关闭？**

**——“干你亲娘！”**

![](https://raw.githubusercontent.com/Pockies/pic/master/(55).png)

当场用[Gitalk](https://gitalk.github.io/)替换掉垃圾[Disqus](https://disqus.com/)。

替换后的评论区基于GitHub的Issue，**没有广告，国内直连，加载迅速，还支持Markdown。**

这也意味着我的整个Blog，现在从网页，到图床，再到评论区，全部依托于GitHub功能。

就连备份也靠的是OneDrive。

**——“啊！巨硬！”**

——**“再生父母！”**

但遗憾的是，以前读者评论在Disqus的内容**无法迁移**，只能丢失......

所以。

**最后对曾在本Blog受过广告侵扰的朋友，以及评论区迁移后评论消失的朋友。**

**——表示非常抱歉。**

~~*※鉴于本人并不是纸片美少女，道歉就不露出胸部了。*~~