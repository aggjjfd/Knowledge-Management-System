> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.right.com.cn](https://www.right.com.cn/forum/thread-199299-1-1.html) ![](https://www.right.com.cn/forum/uc_server/data/avatar/000/27/04/92_avatar_middle.jpg)iSkyun  _ 本帖最后由 iSkyun 于 2016-11-18 11:12 编辑_  
首先可以在百度百科了解到什么是 “[**NAT**](http://baike.baidu.com/item/nat)”，传送门→“[**NAT 科普**”](http://baike.baidu.com/item/nat)  
然后呢，看了那么多我们大概就知道了一些关于 NAT 的基本知识，比如说 “[**定义**](http://baike.baidu.com/item/nat)”、“[**功能**](http://baike.baidu.com/item/nat#1)”、“[**实现方式**](http://baike.baidu.com/item/nat#2)” 及 “[**类型**](http://baike.baidu.com/item/nat#7)”  
提升 NAT 类型的好处：  
浏览网页、观看视频、游戏等更顺畅，下载速度更稳定快速，  
特别是对那些玩 ED2K/PT 下载、PS4/XBox 主机游戏的，  
提升 NAT 类型后更有可能获取到 HigtID、更容易进入游戏房间连线等。  
好了，废话有点多了。  
要提升 NAT 类型，我们必须知道 NAT 的 4 个类型：NAT1、NAT2、NAT3、NAT4。  
它们分别对应（详情见[百度百科](http://baike.baidu.com/item/nat#7)）：  
**NAT1** → **Full Cone** NAT  
**NAT2** → **Address-Restricted Cone** NAT  
**NAT3** → **Port-Restricted Cone** NAT  
**NAT4** → **Symmetric** NAT  
说些比较重要的前话：路由器少一层是一层，这样越有可能得到 NAT1 和 NAT2 这两类 NAT 类型。  
一般建议家里的网路是以下两种拓扑类型：  
1、光猫桥接→主路由（拨号连接外网用）→副路由（纯 AP 模式，扩展信号）  
2、光猫拨号（直接充当主路由）→副路由（纯 AP 模式，扩展信号）  
这样的好处是桥接和纯 AP 是不进行 NAT 的，而是 SWitch，所以不会导致多一层 NAT。  
如果你的网络是 NAT1，那这是最宽松的网络环境，你想做什么，基本没啥限制；  
如果是 NAT4 的话，这是最严格的网络环境，可能会玩不了游戏、下载都没速度；  
一般，我们家里的设备都是通过光猫桥接 + 无线路由器拨号的形式连接到外网的，  
此时，基本是 NAT2 和 NAT3，正常情况对看网页、游戏及下载都没有过多的限制。  
但是，现在个别网络游戏严格要求你的网络环境必须是 “**NAT2**” 以上（NAT2 和 NAT1），才能进行游戏。  
而你的网络环境又是 "NAT3” 及 “NAT4", 那到底该怎么办呢？  
下面我们介绍一些简单提升 NAT 类型的方法，其实就是进行 [**NAT 穿透**](http://baike.baidu.com/item/nat#3_3)（[NAT Traversal](http://baike.baidu.com/item/nat#3_3)）：  
1、如果你的路由器有启用 “**Full Cone”、“STUN”、“TURN”、“ICE”、“uPnP”** 等功能，果断都启用了。  
如果没有的话，你的路由器差不多可以扔了，因为现在的路由器 **“uPnP”** 基本是标配，连这都没有，那你的路由器是有多古董。  
2、如果你的路由器没有以上功能，那可以找下有没有 **“**[DMZ](http://baike.baidu.com/item/dmz)**”** 功能（什么是 “DMZ”，请问度娘 → [DMZ](http://baike.baidu.com/item/dmz) ）,  
有的话，可以启用它，并把你要提升 NAT 类型的主机 IP 地址设置好。  
（一般建议有 “Full Cone”、“uPnP” 等，就不要开 "DMZ”了，除非你是 PS4/XBox 这类游戏主机要提升 NAT 类型）  
3、在 Windows 上把以下三个服务设置为自动启动，并启动该服务：  
一般这三个服务都会被奇虎 360 等带启动项优化的软件当做无用启动项**被 “优化”** 成禁止启动。  
怎么手动设置为自动启动，并启动，详情问 → [**度娘**](https://zhidao.baidu.com/question/209154882.html)  
Function Discovery Provider Host  
Function Discovery Resource Publication  
SSDP Discovery  
4、在 Windows 防火墙，放行你需要提升 NAT 类型的软件或者游戏程序（EXE 程序或者 UWP 程序），  
如果你不会放行，也可以直接关闭 Windows 防火墙。（一般不推荐这样做，还是老话，不懂问 “[**度娘**](https://zhidao.baidu.com/question/1735570524535246787.html)”）  
第 4 步很重要，这步没做，等于其它的全是在做无用功。  
5、如果你的设备是通过电脑共享网络的形式上网的，建议把这个服务也打开：UPnP Device Host  
以上，能弄的都弄了，这样你的网络环境就会越好，甚至 NAT1 都没有问题。  
这是我通过以上设置，进行 NAT 穿透 + 公网 IP 一枚，测得的结果：  
![](data/attachment/forum/201611/10/132059dd4rfiilqz4e4s4p.jpg)

**捕获. JPG** _(17.09 KB, 下载次数: 146)_

[下载附件](forum.php?mod=attachment&aid=MTQzODYyfGZhOWM3Zjc3fDE2NDQzMjk0NDd8MHwxOTkyOTk%3D&nothumb=yes)  [保存到相册](javascript:;)

2016-11-10 13:20 上传

  
妥妥的 NAT1  
最后附上 NAT 类型测试工具：  
 ![](https://www.right.com.cn/forum/static/image/filetype/zip.gif) [NAT 类型测试. zip](forum.php?mod=attachment&aid=MTQzODYzfDBkMzEwZjVkfDE2NDQzMjk0NDd8MHwxOTkyOTk%3D) _(490.51 KB, 下载次数: 10441)_ 2016-11-10 13:26 上传 点击文件名下载附件  
NAT 类型检测工具  
P.S.:  
1、如果能找运营商要到外网 IP，这是最好的，没有公网 IP 的话可以打电话给客服，  
说 “我家的宽带怎么没有公网 IP 啊，我需要在家里安装远程监控，没有公网 IP 的话不行，如果不给我公网 IP，我只好退宽带换别家的了。”  
态度强硬点，最好一开始就把客服的工号也要了，说完上面的，再补上 “不给就投诉你。”；  
2、还有一种最笨的就是直接电脑拨号上网，Windows 直接把防火墙关了，只要你的是公网 IP，妥妥的基本都是 NAT1；  
3、如果要不到公网 IP，能提升到 NAT2，这样也很不错了；  
4、如果你是要提升 PS4/XBox 这类游戏主机的 NAT 类型，建议以上能做的都做了。  
![](https://www.right.com.cn/forum/uc_server/data/avatar/000/32/12/92_avatar_middle.jpg)1980490718  支持一下。。。![](https://www.right.com.cn/forum/uc_server/images/noavatar_middle.gif)yymp3  多谢分享教程 ![](https://www.right.com.cn/forum/uc_server/data/avatar/000/35/52/99_avatar_middle.jpg) ks12345678 感谢分享！辛苦了 ![](https://www.right.com.cn/forum/uc_server/images/noavatar_middle.gif) pbt79 这种文章需要支持，加油 ![](https://www.right.com.cn/forum/uc_server/images/noavatar_middle.gif) zxh5806 科普知识看看来了 ![](https://www.right.com.cn/forum/uc_server/data/avatar/000/19/37/47_avatar_middle.jpg) raul222 我来检测看看  玩游戏 ![](https://www.right.com.cn/forum/uc_server/images/noavatar_middle.gif) ajtolqrw   
支持一下。。。![](https://www.right.com.cn/forum/uc_server/data/avatar/000/31/36/03_avatar_middle.jpg)wzn1010  菜鸟一枚前来学习![](https://www.right.com.cn/forum/static/image/smiley/default/biggrin.gif) ![](https://www.right.com.cn/forum/uc_server/data/avatar/000/05/03/42_avatar_middle.jpg) nieccyyy 恩，涨知识了……![](https://www.right.com.cn/forum/uc_server/images/noavatar_middle.gif)hzlryo0919  尝试一下，被这个问题困扰很久了 ![](https://www.right.com.cn/forum/uc_server/images/noavatar_middle.gif) Ryan31 谢谢分享![](https://www.right.com.cn/forum/static/image/smiley/default/smile.gif) ![](https://www.right.com.cn/forum/uc_server/images/noavatar_middle.gif) ionlin asdasdasdasdas![](https://www.right.com.cn/forum/uc_server/data/avatar/000/18/46/69_avatar_middle.jpg)496175433  感谢分享！![](https://www.right.com.cn/forum/uc_server/data/avatar/000/33/29/89_avatar_middle.jpg)zhl416  6666 看看先