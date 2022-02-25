> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [bbs.archlinuxcn.org](https://bbs.archlinuxcn.org/viewtopic.php?id=11584)

> 机型 thinkpad x1 nano 显卡 Intel® Iris Xe Graphics 桌面 gnome 目前主用浏览器 chrome

#1 [2021-08-27 21:11:34](https://bbs.archlinuxcn.org/viewtopic.php?pid=48403#p48403)
------------------------------------------------------------------------------------

**chen05_20**

**会员**

注册时间： 2021-04-02

帖子： 79

### 关于浏览器视频播放问题的一些探索

机型 thinkpad x1 nano  
显卡 Intel® Iris Xe Graphics  
桌面 gnome  
目前主用浏览器 chrome

最近换了 4k 的显示器，发现浏览器在播放视频的时候不是很流畅，一开始以为是风扇的问题，后来有人指出是没有用硬件加速，然后就在这个问题上开始一些探索，主要参考 wiki 和这个帖子 [https://zhuanlan.zhihu.com/p/219715236](https://zhuanlan.zhihu.com/p/219715236)

首先 mpv 硬解播放视频是可以实现的，但是要想用在浏览器上就很麻烦了，为了测试，我还特地开了个 b 站大会员  
首先发现 chrome 上不管怎么操作都无法使用硬件加速，Chromium 仅可以在 xorg 的模式下开启硬件加速，这个硬件加速有 2 个问题，一是 gpu 效率利用太低，看一个 4k120fps 的视频 (不开弹幕)，gpu 只能吃 20 几，然后看视频各种掉帧，二是不知道啥原因，只要开了弹幕，不管播放的是不是 4k 的视频，帧数都会立刻降到 10 几。所以现在想求助几个问题  
1. 目前其实用 chrome 软解已经可以应对所有 4k 以下的视频了，但风扇扇的不快倒是挺让我担心散热的，然而 chrome 和 Chromium 硬解的性能确存在差异，打开内置的 fps 实时帧数，发现 chromefps 很少能到 50 以上, 大概在 45 左右徘徊，然而 Chromium 确可以达到平均 57 左右  
2.Chromium 在 xorg 的模式下的硬件加速还有没有改进的方法，总感觉这个开了还不如不开  
3. 关于 xwayland 下，我查到火狐的浏览器是可以实现硬件加速的，但是我按照教程，依然无法实现硬件加速 (合成器 WebRender 参数 WEBRENDER 为     
available by default  
force_enabled by user: Force enabled by envvar  
disabled by env: Not qualified)，有人知道为啥么，或者弄成功的能不能分享以下经验；

#2 [2021-08-27 21:33:53](https://bbs.archlinuxcn.org/viewtopic.php?pid=48404#p48404)
------------------------------------------------------------------------------------

**依云**

**会员**

![](https://bbs.archlinuxcn.org/img/avatars/159.png?m=1336986592)

所在地： a.k.a. 百合仙子

注册时间： 2011-08-21

帖子： 6,847

[个人网站](https://blog.lilydjwg.me/)

### Re: 关于浏览器视频播放问题的一些探索

我的 Google Chrome 开启硬件加速没问题，运作效率不清楚。  
我的火狐开启硬件加速没问题（X11），但是效率比 mpv 低不少，GPU render 会占满。  
不要在 xwayland 下跑火狐。直接在 wayland 下跑不好么。  
YouTube 视频 4k、8k 都可以免费看的。

#3 [2021-08-28 15:55:38](https://bbs.archlinuxcn.org/viewtopic.php?pid=48405#p48405)
------------------------------------------------------------------------------------

**chen05_20**

**会员**

注册时间： 2021-04-02

帖子： 79

### Re: 关于浏览器视频播放问题的一些探索

依云 说：

> 我的 Google Chrome 开启硬件加速没问题，运作效率不清楚。  
> 我的火狐开启硬件加速没问题（X11），但是效率比 mpv 低不少，GPU render 会占满。  
> 不要在 xwayland 下跑火狐。直接在 wayland 下跑不好么。  
> YouTube 视频 4k、8k 都可以免费看的。

你的 chrome 版本是？我是装的 archlinux 下的那个 另外目前 chrome 在 wayland 下的视频加速还是不支持的么？

我事先并不清楚 xwayland 是咋回事，只是在 wayland 下，按照 wiki 跑进来窗口协议就是 xwayland.... 就顺口说了

_最近编辑记录 chen05_20 (2021-08-28 15:56:03)_

#4 [2021-08-28 16:36:11](https://bbs.archlinuxcn.org/viewtopic.php?pid=48406#p48406)
------------------------------------------------------------------------------------

**依云**

**会员**

![](https://bbs.archlinuxcn.org/img/avatars/159.png?m=1336986592)

所在地： a.k.a. 百合仙子

注册时间： 2011-08-21

帖子： 6,847

[个人网站](https://blog.lilydjwg.me/)

### Re: 关于浏览器视频播放问题的一些探索

google-chrome 92.0.4515.159-1，不知道「archlinux 下的那个」是哪个，Google Chrome 难道不止一个么。Wayland 我不了解。好像连输入中文都成问题的说。  
火狐设置一个环境变量之后可以直接在 wayland 下跑，不需要兼容层。