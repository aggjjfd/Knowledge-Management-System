> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.zhullyb.top](https://blog.zhullyb.top/2021/09/05/wrong-fonts-color-fix-under-kde-with-a-dark-theme/)

> 9 月 6 日更新：AUR 的 wemeet-bin 维护者 sukanka 已经将咱的运行指令直接打进了包内，故本文已经基本失去原本的应用意义，但仍可以作为一个案例来解决类似问题。

**9 月 6 日更新：AUR 的`wemeet-bin`维护者 sukanka 已经将咱的运行指令直接打进了包内，故本文已经基本失去原本的应用意义，但仍可以作为一个案例来解决类似问题。**

> 在使用腾讯最近推出的 Linux 原生腾讯会议的时候，咱遇到了个十分影响体验的问题。
> 
> 我在使用 KDE 的暗色主题，腾讯回忆自作主张将字体颜色调成了白色。然而，字体背景是白色的没，因此导致对比度下降，字体难以辨认。效果大概是这个鬼样子:
> 
> [![](https://npm.elemecdn.com/superbadguy-bed@0.0.5/18.png)](https://npm.elemecdn.com/superbadguy-bed@0.0.5/18.png)

然而我一时半会儿却找不到合适的变量在运行腾讯会议之前 unset，无法指定它使用一个正确的字体颜色。

此时，我想到了 fakehome 的解决方案——bwrap。

关于 bwrap，依云在 ta 的[博客](https://blog.lilydjwg.me/2021/8/12/using-bwrap.215869.html)里讲过运行原理，我在这里直接摘一小段过来

> bwrap 的原理是，把 / 放到一个 tmpfs 上，然后需要允许访问的目录通过 bind mount 弄进来。所以没弄进来的部分就是不存在，写数据的话就存在内存里，用完就扔掉了。

而我们要做的，就是开一个 tmpfs 作为`$HOME/.config`，让腾讯会议读取不到 KDE 的主题配置文件。

使用如下命令

<table><tbody><tr><td></td><td><pre>bwrap --dev-bind / / --tmpfs $HOME/.config wemeet

</pre></td></tr></tbody></table>

软件启动确认没有问题后，我们可以更改腾讯会议 desktop 中的启动命令

```
sudo $EDITOR /usr/share/applications/wemeetapp.desktop
```

将`Exec=`后面的命令改成我们刚刚启动所使用的命令即可。

> 关键词: bwrap, linux, 暗色模式, 深色模式, 夜间模式, 白色字体, 亮色字体