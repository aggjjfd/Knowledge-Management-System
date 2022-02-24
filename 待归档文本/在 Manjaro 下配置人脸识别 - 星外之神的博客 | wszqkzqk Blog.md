> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [wszqkzqk.github.io](https://wszqkzqk.github.io/2021/08/17/%E5%9C%A8Manjaro%E4%B8%8B%E9%85%8D%E7%BD%AE%E4%BA%BA%E8%84%B8%E8%AF%86%E5%88%AB/)

> 天下难事，必作于易；天下大事，必作于细

在 Manjro 上配置人脸识别的缘由[](#在manjro上配置人脸识别的缘由)
-----------------------------------------

我的系统登录密码设置得太长了，而且各种字母数字特殊符号，输入起来很麻烦  
想到 Windows 系统下有 Windows Hello™，由此，我决定用人脸识别来解决这个问题  
就是找 Linux 下 Windows Hello™的替代品（

过程[](#过程)
---------

我的设备是联想小新 Pro 16 集显版，系统环境是 Manjaro KDE  
[![](https://wszqkzqk.github.io/img/manjaro-screenfetch.webp)](https://wszqkzqk.github.io/img/manjaro-screenfetch.webp) 由于硬件太新，主线内核中没有我的无线网卡（RTL8852AE）的驱动，这台电脑又没有网线接口，我只能临时将手机通过 USB 连接的方式共享网络给电脑，安装好对应版本的 linux-header 后，在 AUR 中下载编译对应的网卡驱动，解决了网卡驱动问题  
[![](https://wszqkzqk.github.io/img/RTW8852AE-driver.webp)](https://wszqkzqk.github.io/img/RTW8852AE-driver.webp) 不知道主线内核什么时候跟进，现在这个驱动稳定性实在是太菜了……

*   2022.01.25 更新：现在在 Linux Kernel 5.16 已经集成了 RTW8852AE 的驱动，不需要折腾了～

能够顺利联网以后，再来考虑人脸识别的问题

事实上，Linux 下的确有一个与 Windows Hello™类似的人脸识别系统——[Howdy](https://github.com/boltgolt/howdy)  
这个项目在 GitHub 上已经拥有 2800 + 颗星（截至 2021.08.17）  
[![](https://wszqkzqk.github.io/img/howdy.webp)](https://github.com/boltgolt/howdy)

### 下载、编译、安装[](#下载编译安装)

该软件在 [GitHub 上的页面](https://github.com/boltgolt/howdy)已经对其安装过程有所介绍

Manjaro 是基于 Arch 开发的衍生发行版，所以可以参考 [Arch Wiki](https://wiki.archlinux.org/title/Howdy_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)) 上的相关内容

理论上可以直接在 Manjaro 自带的软件管理器 Pamac 上直接搜索并安装 howdy, 然而由于 howdy 的源代码存储在 GitHub 上，在大陆访问网络并不通畅，很可能会出现下载失败的情况，所以这里我建议中国大陆的 Linuxer 采用另外的方法：

先在工作目录打开终端，执行：

```
git clone https://aur.archlinux.org/pam-python.git
git clone https://aur.archlinux.org/python-dlib.git
git clone https://aur.archlinux.org/python-face_recognition_models.git
git clone https://aur.archlinux.org/python-face_recognition.git
git clone https://aur.archlinux.org/howdy.git


```

[![](https://wszqkzqk.github.io/img/aur-git-clone.webp)](https://wszqkzqk.github.io/img/aur-git-clone.webp)

然后再在各个软件的 AUR 页面中分别找到主要的源文件的地址（编译时能够直接下载成功的就不用找了，无须每个都找），用 GitHub 文件下载神器——[Free Download Manager](https://www.freedownloadmanager.org/) 下载（[FDM 的 AUR 在这里](http://aur.archlinux.org/packages/freedownloadmanager)） [![](https://wszqkzqk.github.io/img/FDM-download.webp)](https://wszqkzqk.github.io/img/FDM-download.webp)

下载完成后，把各个软件包所需的文件分别移动到各个已经从 AUR 上 clone 下来的文件夹中（注意：有些文件在 FDM 中下载的名称与 pkgbuild 中的不同，需要重命名）

在各个文件夹中执行:

注意：

*   要按照 pam-python、python-dlib、python-face_recognition_models、python-face_recognition、howdy 的顺序进行安装, 否则将会提示无法满足依赖
*   当 Python 版本更新后，需要重新构建这几个软件包（由于 Python 目录在更新之后会发生改变，如果没有重新构建，则 howdy 在调用库时会由于新路径下没有所需要的库而无法运行）

[![](https://wszqkzqk.github.io/img/makepkg.webp)](https://wszqkzqk.github.io/img/makepkg.webp) 安装过程到此结束

### 配置[](#配置)

在 Arch Wiki 上已有 howdy 的[配置教程](https://wiki.archlinux.org/title/Howdy_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))，但是按照其方法进行配置后在 KDE 上仍然不能使用人脸识别登录，在此，我给出一个更完善的方法：

#### 红外发射装置的启用（如果不需要或设备不支持红外发射可跳过此过程）[](#红外发射装置的启用如果不需要或设备不支持红外发射可跳过此过程)

首先，对于支持红外发射的电脑，墙裂建议开启红外发射功能提高识别的准确度与安全性（而且红外发射式还支持全黑暗状态下的人脸识别）

若需启用红外发射，需要安装 [linux-enable-ir-emitter](https://github.com/EmixamPP/linux-enable-ir-emitter)

```
git clone https://aur.archlinux.org/linux-enable-ir-emitter.git
cd linux-enable-ir-emitter
makepkg -si


```

如果出现下载失败的情况，按照上一章的方法下载即可

安装完成后，执行如下命令：

```
sudo linux-enable-ir-emitter configure
sudo linux-enable-ir-emitter boot enable


```

按照终端中的提示完成该过程即可，配置过程中程序会尝试以不同方式启动电脑的红外发射装置，若成功启动则输入`yes`，未成功启动则输入`no`，逐项尝试直到成功即完成了配置过程。如果部分电脑的红外发射装置所发出的光肉眼完全不可见，也可以使用手机的相机来检测；有时候可能能观察到红外发射但是仍然无法使用，这时也可以重新运行`sudo linux-enable-ir-emitter configure`进行切换。此外，配置时应尽量选择与 Windows Hello™效果相同的发射模式在再输入`yes`。（如 Windows Hello™下红外发射器为闪烁状态，则应尽量选择使红外发射器闪烁的配置而不选择使其常亮的配置）

#### PAM 配置[](#pam配置)

要启用人脸验证功能，需要在`/etc/pam.d/`目录下的部分文件插入：

```
auth sufficient pam_python.so /lib/security/howdy/pam.py


```

将以上代码插入到所需要改动的文件的**第二行**，**切勿插入至第一行，切勿删除或改动文件的其他内容**

一般而言，需要插入的文件如下，可自行按具体需要进行调整

<table><thead><tr><th>文件</th><th>功能</th></tr></thead><tbody><tr><td>login、system-local-login、sddm（如果使用的是 lightdm 或者 gdm 则是其对应的文件）</td><td>在用户登录时启用人脸识别</td></tr><tr><td>kde（如果使用的是其他桌面环境则是其对应文件）</td><td>在桌面环境所提供的锁屏界面中启用人脸识别</td></tr><tr><td>sudo、polkit-1</td><td>在授权验证中启用人脸识别</td></tr></tbody></table>

插入后的示例：`/etc/pam.d/sudo`

```
#%PAM-1.0
auth    sufficient pam_python.so /lib/security/howdy/pam.py
auth		include		system-auth
account		include		system-auth
session		include		system-auth


```

#### 找出相机在系统中的文件地址[](#找出相机在系统中的文件地址)

对一般的笔记本，有红外相机的是在`/dev/video2`，无红外的是在`/dev/video0`

如果不确定红外相机的位置，可以安装 Skanlite 这款软件:`sudo pacman -Su skanlite` [![](https://wszqkzqk.github.io/img/skanlite.webp)](https://wszqkzqk.github.io/img/skanlite.webp) 通过逐一测试筛选出列表中的红外相机（红外相机一般呈现出来的是光影看起来特别奇怪的黑白照片）

#### Howdy 配置[](#howdy配置)

得知了红外相机的文件位置后在终端中执行：

找到`device_path = none`一行，将`device_path =`后面的参数改为相机的文件位置，例如： [![](https://wszqkzqk.github.io/img/howdy-config.webp)](https://wszqkzqk.github.io/img/howdy-config.webp)

编辑完成后，同时按下 Ctrl + X 键保存并退出

由于大多数桌面环境内置的锁屏界面（不是指 DM 的登录界面）并未以 root 身份运行，而 howdy 的文件在默认状态下对非 root 用户不可读，故此时锁屏界面无法启用人脸识别，这一问题可以通过更改权限解决：

```
chmod -R 755 /lib/security/howdy


```

**注意：**

*   无论是 SDDM（或其他 DM）中还是桌面环境自带的锁屏界面中，人脸识别都并非是像 Windows Hello™中那样自动启动，若需要使用人脸识别登录，需要敲击 Ether 键或点击登录按钮（无需输入密码）
*   在添加了 pam 的各场景中，默认优先使用人脸识别进行验证，若验证失败，也可输入密码进行验证
*   polkit-1 这样的 GUI 授权验证工具会在使用人脸识别时同步弹出密码框，此时人脸识别已经启用，不需要任何输入即可完成验证，也无需点击确认密码的按钮，若人脸识别失败，同样可以使用密码验证

#### 添加人脸信息[](#添加人脸信息)

打开终端，执行：

按照提示，为所设置的人脸信息输入一个不超过 24 字的标识，然后盯着相机即可

如果要清除所有已保存的人脸信息，执行：

#### 完成后的其他配置[](#完成后的其他配置)

KDE 钱包（软件名字非常奇怪，这个与钱无关，是个密码管理软件，不如叫 KDE 钥匙包 QwQ）的自动打开功能在使用人脸识别登录时会失效，这将会导致 WiFi 密码、Chromium 系浏览器存储的密码在未进行 KDE 钱包验证时无法使用

为了避免输密码的麻烦又引入了新的输密码的步骤当然是不合理的……

但还好可以取消 KDE 钱包的密码验证，方法如下：

*   打开 KDE 钱包**管理器**
*   点击 “更改密码”
*   将两行均留空，点击确认即可

[![](https://wszqkzqk.github.io/img/kdewalletmanager.webp)](https://wszqkzqk.github.io/img/kdewalletmanager.webp) 当然，将密码留空用有一定的风险，因此，建议开启 KDE 钱包的 “访问控制” 功能保障安全 [![](https://wszqkzqk.github.io/img/kdewallet.webp)](https://wszqkzqk.github.io/img/kdewallet.webp) 开启访问控制后，应用访问 KDE 钱包时将会弹出提醒; 对于 KDE 本身（用于 WiFi 密码存储和其他用途）、Chromium 系浏览器等可信软件，可以直接授予永久访问权限，不必每次都在弹出窗口中确认

免责声明[](#免责声明)
-------------

本博客仅为方法分享，不承担任何责任，按照本博客内容操作所产生的各种风险均由操作者自行承担

捐赠[](#捐赠)
---------

如果您希望对本网站的维护予以支持，欢迎捐赠！

欢迎大家在评论区留言！

转载授权声明[](#转载授权声明)
-----------------

本文采用[署名 - 非商业性使用 - 相同方式共享 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh) 协议发布，未经本人许可，**禁止用于商业用途**，非商业转载时请**对本文原作者进行署名**，基于本文的衍生作品需要按照[相同方式共享](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh)

* * *