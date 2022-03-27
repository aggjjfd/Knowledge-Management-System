# 开启 archlinux 下的 chrmium 视频播放 GPU 加速
> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [zhuanlan.zhihu.com](https://zhuanlan.zhihu.com/p/219715236)

2020 年 10 月 8 日更新：chromium 升级到 86 之后，需要再在 `~/.config/chromium-flags.conf`文件中增加`一个 flag`--enable-accelerated-video-decode`

archlinux 下的 chromium，默认在播放在线视频时都不开启 GPU 加速，于是在 xps13 这样的超极本上看在线视频总是风扇狂转，CPU 温度六七十。

chromium 中可以用 GPU 加速的功能有很多，除了那些在 Intel i7-8565U 上已经默认启用的，这里介绍三项需要手动开启的功能。

以下方法在 archlinux，5.4/5.8 内核，chromium 包（85.0.4183.83-1），Intel i7-8565U 上测试通过。

首先是打开浏览器内视频播放的 GPU 加速，比如 youku 视频，方法如下:

1.  启用硬件视频加速。参考[这篇 archwiki](https://wiki.archlinux.org/index.php/Hardware_video_acceleration#Intel)，对于 Broadwell(2014 年推出) 之后的 intel CPU，安装`intel-media-driver`包。安装完成后可以执行`vainfo`（需要安装`libva-utils`包）来验证结果，如果命令不返回任何错误，可以看到 GPU 对各种视频格式加速的支持情况。另外也可以用 mpv 这个播放器来检验 GPU 加速是否开启：执行`mpv --hwdec=auto-safe video-file-name`，查看终端输出是否包含`Using hardware decoding (vaapi)`
2.  在 chromium 地址栏上输入：`chrome://flags`，搜索`Override software rendering list`，把默认的`Disabled`改为`Enabled`
3.  创建`~/.config/chromium-flags.conf`文件，加入`--use-gl=desktop`作为 chromium 的 command line flag。

> 注 1：如果用的不是 chromium 包，而是 google-chrome 这个 aur, 则需要使用`~/.config/chrome-flags.conf`文件  
> 注 2：在`chrome://flags`里设置`Override software rendering list`这个操作照理也应该可以通过给 chromium 添加`--ignore-gpu-blacklist`实现，然而在当前 chromium 版本中，在`~/.config/chromium-flags.conf`里添加这个 flag 并没有发挥作用  
> 注 3: `--use-gl=desktop`仅在 xorg 中有效，如果用的是 XWayland，则需要使用`--use-gl=egl`  

这时可以打开 chromium 的 developer tools，检验播放 youku 视频时 GPU 加速是否开启，如下图：播放 youku 视频，按`Control-Shift-i`进入开发者工具，点击右上角齿轮按钮 ->`Experiments`，开启`Media Elements Inspection`。然后点击右上角三个竖点 ->`More Tools`->`Media`，就可以看到多出来的`Media`标签页，在里面可以看到`Players`-> 视频所在浏览器标签名称 ->`Video Decoder`，里面的`Decoder Name`是`MojoVideoDecoder`，`HardwareDecoder`为`true`。这就表示 GPU 加速打开了。可以观察到播放 youku 视频时，CPU 温度降低了 10 度左右，CPU 利用率也从 100% 左右降低到 30-60%。

![](https://pic4.zhimg.com/v2-02af8eac857b584cd22561b891c25d93_r.jpg)

chromium 中可以用 GPU 加速的第二个功能：根据[这篇文章](https://www.ghacks.net/2017/01/31/chromes-rendering-gets-faster-here-is-what-google-does-not-tell-you/)，chrome 多了一个 zero-copy 的技术，可以加速页面渲染 35%。启用方法：在`~/.config/chromium-flags.conf`里添加`--enable-zero-copy`作为 chromium 的 command line flag。

检验结果：打开在 chromium 地址栏上输入：`chrome://gpu`，可以在`Compositor Information`->`Tile Update Mode`里看到`Zero-copy`。然而 35% 提速并没有明显体验到。

chromium 中可以用 GPU 加速的第三个功能：默认情况下在 chromium 地址栏上输入：`chrome://gpu`，可以看到`Graphics Feature Status`里的`Rasterization`为`Software Only`，可以在`~/.config/chromium-flags.conf`里加入`--enable-gpu-rasterization`，这样`Rasterization`就会变成`Hardware accelerated on all pages`。该项加速有什么优势日常使用中并不明显。