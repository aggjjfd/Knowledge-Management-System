> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.zhihu.com](https://www.zhihu.com/question/46525639/answer/157272414) ![](https://pic1.zhimg.com/v2-3177914b9b48abc693b1ae5ae36b5c00_xs.jpg?source=1940ef5c)滑稽

今天装完 Ubuntu 恰好碰到这个问题，这里写出解决方法。

先说下两个概念：

UTC 即 Universal Time Coordinated，协调世界时（[世界统一时间](https://link.zhihu.com/?target=http%3A//baike.baidu.com/link%3Furl%3DHnX2f1XGSuotBE1y-885nj2eeiyHnFBdgWHP_f0hCNDSHO9kUbSSNDaYDJ9BQ4p5JUzMhZfbPKv76FkHnZ5CtPgACZ5uVpz3R48L_SDVcQr0Q7jI75gXTkKwerfz1sOY8VFrTL0ddG-NmmwxIfXFSK)）

GMT 即 Greenwich Mean Time，格林尼治平时

Windows 与 Mac/Linux 看待系统硬件时间的方式是不一样的：

Windows 把计算机硬件时间当作本地时间 (local time)，所以在 Windows 系统中显示的时间跟 BIOS 中显示的时间是一样的。

Linux/Unix/Mac 把计算机硬件时间当作 UTC， 所以在 Linux/Unix/Mac 系统启动后在该时间的基础上，加上电脑设置的时区数（ 比如我们在中国，它就加上 “8” ），因此，Linux/Unix/Mac 系统中显示的时间总是比 Windows 系统中显示的时间快 8 个小时。

所以，当你在 Linux/Unix/Mac 系统中，把系统现实的时间设置正确后，其实计算机硬件时间是在这个时间上减去 8 小时，所以当你切换成 Windows 系统后，会发现时间慢了 8 小时。就是这样个原因。

  

OK！既然知道原因了，就好解决了。

这里提供两种解决方法:

1. 在 Ubuntu 中把计算机硬件时间改成系统显示的时间，即禁用 Ubuntu 的 UTC。

这又有另一个需要注意的地方：

在 Ubuntu 16.04 版本以前，关闭 UTC 的方法是编辑 / etc/default/rcS，将 UTC=yes 改成 UTC=no， 但在 Ubuntu 16.04 使用 systemd 启动之后，时间改成了由 timedatectl 来管理，所以更改方法是

  

```
timedatectl set-local-rtc 1 --adjust-system-clock


```

执行后重启 Ubuntu，应该就没有问题了。

  

2. 修改 Windows 对硬件时间的对待方式，让 Windows 把硬件时间当作 UTC.

打开命令行程序，在命令行中输入下面命令并回车

  

```
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1


```

应该就没有问题了。

  

这两种方法，我个人倾向于使用第一种。

![](https://pic1.zhimg.com/50/7f2e7bd937daeeca641d15097f9198f0_720w.jpg?source=1940ef5c)
