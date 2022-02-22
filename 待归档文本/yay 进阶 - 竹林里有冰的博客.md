> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.zhullyb.top](https://blog.zhullyb.top/2021/04/04/yay-more/)

> yay 是一个 AUR Helper，他可以执行 pacman 的几乎所有操作，并在此基础上添加了很多额外用法。

> yay 是一个 AUR Helper，他可以执行 pacman 的几乎所有操作，并在此基础上添加了很多额外用法。
> 
> 我没有在网络上查找到关于 yay 的、除了 pacman 基础用法和安装 AUR 包以外的中文教程，英文的也几乎没有看到，这也是我写这篇文章的原因所在。
> 
> 本文通篇详讲 yay 的每一个设置 / 选项（大概就是 archwiki 那种干涩的行文思路），最后会给出我自己的一些常用命令，但不会做解释。
> 
> 写作时参考了 yay 的英文使用手册，如果你的 arch 安装了 yay，那么即可通过`man yay`命令随时查阅它。

**Tips1: 本文中出现的 foo 一般是指包名，标注 * 的表示该选项默认启用。**

**Tips2: 使用电脑端的访客可以在侧栏以获取目录。**

[](#基本用法 "基本用法")基本用法[](#基本用法)
-----------------------------

yay 的基本用法是`yay <operation> [options] [targets]`、`yay foo`和`yay`，`yay <operation> [options] [targets]`的用法可以讨论的点比较多，我会在后文中一一道来。

### [](#yay "yay")`yay`[](#yay)

当我们仅执行`yay`，后面不跟任何参数时，yay 会执行操作`yay -Syu`，他会先调用 pacman 更新源的数据库、更新所有从源内安装的软件包，并检查你的 AUR 包有没有更新。

### [](#yay-foo "yay foo")`yay foo`[](#yay-foo)

通过 yay 后面直接跟包名的命令会让 yay 直接在源和 AUR 内搜索带有`foo`关键词的包（包名和简介中只要出现 foo 都会被一网打尽），以下是我执行`yay dingtalk`的输出

<table><tbody><tr><td></td><td><pre>5 aur/com.dingtalk.deepin 5.0.15deepin7-1 (+0 0.00)
    Deepin Wine dingtalk
4 aur/deepin.com.dingtalk.com 5.1.28.12-2 (+1 0.12)
    DingTalk Client on Deepin Wine
3 aur/dingtalk 2.1.3-1 (+3 0.00)
    钉钉桌面版，基于electron和钉钉网页版开发，支持Windows、Linux和macOS
2 aur/dingtalk-linux 3.5.5-1 (+6 0.12)
    May be the official Linux experimental version
1 aur/dingtalk-electron 2.1.9-1 (+9 0.15)
    钉钉Linux版本
==&gt; Packages to install (eg: 1 2 3, 1-3 or ^4)
==

</pre></td></tr></tbody></table>

输入每一项对应的序号即可进入相应的安装过程。

### [](#yay-lt-operation-gt-options-targets "yay <operation> [options] [targets]")`yay <operation> [options] [targets]`[](#yay-lt-operation-gt-options-targets)

在这里，<operation> 每次只能有一个，[options]和 [targets] 可以有多个，且多个 [options] 可以合起来写在一起。比如`yay -P -s -f`可以直接写成`yay -Psf`，顺序也可以颠倒，`-Psf`和`-sPf`没区别。

#### [](#Y-yay "-Y (--yay)")`-Y (--yay)`[](#Y-yay)

-Y 行为其实是 yay 的默认行为，当你没有加其他的行为参数时，yay 就会执行 - Y 参数，可以跟`--gendb`和`-c`。

##### [](#gendb "--gendb")`--gendb`[](#gendb)

生成 AUR 数据库。**仅当从另一个 AUR Helper 迁移到 yay 时，才应使用此选项。**~（根据我的个人理解，是根据你 Arch 内安装的源内找不到的包的包名去 AUR 里寻找对应的 PKGBUILD，并且把能找到的 PKGBUILD 给 clone 到`~/.cache/yay/`目录下）~

千玄子大佬说：“简单说来就是把在 AUR 的 PKGBUILD 下下来然后比对是否要更新。”

##### [](#c（-clean） "-c（--clean）")`-c（--clean）`[](#c（-clean）)

清除不再需要的、没有被依赖的包。（相当于 apt 中的 autoremove）

#### [](#P-show "-P(--show)")`-P(--show)`[](#P-show)

执行特定的 Print 操作。可以跟的 [option] 有`-c、-f、-d、-g、-n、-s、-u、-w、-q`

##### [](#c-complete "-c(--complete)")`-c(--complete)`[](#c-complete)

Print 所有源内和 AUR 软件包的列表。这是给命令行操作提供的，并不打算由用户直接使用。（意思是启用了这个选项以后你的终端会出现一大串长常的列表来告诉你你的 Arch 到底可以从哪里安装哪些包，并不是直接给你用的，是作为数据留给别的命令来玩耍的）

##### [](#f-fish "-f(--fish)")`-f(--fish)`[](#f-fish)

在输出结果到终端时，会专门为 fish 用户做微调。（但是根据 SamLukeYes 大佬说他用 fish 体验下来并没有感知到加不加有什么区别，应该是属于感知不强的选项）

##### [](#d-defaultconfig "-d(--defaultconfig)")`-d(--defaultconfig)`[](#d-defaultconfig)

Print 默认的 yay 配置。

##### [](#g-currentconfig "-g(--currentconfig)")`-g(--currentconfig)`[](#g-currentconfig)

Print 当前的 yay 配置。

##### [](#n-numberupgrades "-n(--numberupgrades)")`-n(--numberupgrades)`[](#n-numberupgrades)

数一数你现在还有多少 AUR 包待更新。yay 作者不推荐你使用呢，他推荐你用`yay -Qu`或者`wc -l`来代替它。

##### [](#s-stats "-s(--stats)")`-s(--stats)`[](#s-stats)

会展示一大堆信息，如下

```
[zhullyb@Archlinux ~]$ yay -Ps
==> Yay version v10.2.0							    
===========================================
==> Total installed packages: 1240				    
==> Total foreign installed packages: 24		    
==> Explicitly installed packages: 271			    
==> Total Size occupied by packages: 14.3 GiB	    
===========================================
==> Ten biggest packages:						    
wps-office-cn: 990.9 MiB
ttf-sarasa-gothic: 855.5 MiB
linux-firmware: 652.3 MiB
baidunetdisk-bin: 494.7 MiB
com.antutu.benchmark: 412.0 MiB
wine: 402.2 MiB
linux-xanmod-cacule-uksm-cjktty: 324.4 MiB
microsoft-edge-dev-bin: 316.4 MiB
wine-mono: 316.2 MiB
deepin-wine5-i386: 259.5 MiB
===========================================
:: Querying AUR...
 -> Missing AUR Packages:  zhullyb-archlinux-git    
 -> Flagged Out Of Date AUR Packages:  xml2
```

##### [](#u-upgrades "-u(--upgrades)")`-u(--upgrades)`[](#u-upgrades)

展示你所有待更新的包。

##### [](#w-news "-w(--news)")`-w(--news)`[](#w-news)

展示来自 archlinux.org 的新闻。需要注意的是，这里的新闻是具有时效性的，只有在你的 Arch 最后一次更新以后发出来的新闻才会被显示出来。如果你不想要 yay 判断新闻时效性，你可以通过`yay -Pww`（即两个`w`）来获取所有能获得的新闻。

##### [](#q-quiet "-q(--quiet)")`-q(--quiet)`[](#q-quiet)

在输出新闻的时候，仅输出新闻的标题。该功能需要与`-w`连用，即`yay -Pwq`。

#### [](#G-getpkgbuild "-G(--getpkgbuild)")`-G(--getpkgbuild)`[](#G-getpkgbuild)

后跟包名。需要注意的是，如果指定的包不存在于官方源，则无法输出，后跟`-f、-p`参数。

_如果希望仅获取来自 AUR（即排除第三方源的干扰）的 PKGBUILD，后需跟`-a`参数。_

##### [](#f-force "-f(--force)")`-f(--force)`[](#f-force)

强制下载 AUR 中的 PKGBUILD，如果它在 yay 缓存目录已经存在了，那就覆盖它！

##### [](#p-print "-p(--print)")`-p(--print)`[](#p-print)

Print 指定包的 PKGBUILD。

### [](#pacman-拓展用法 "pacman 拓展用法")pacman 拓展用法[](#pacman-拓展用法)

yay 虽然可以使用 pacman 的所有 <operation>，但是它远不仅于此。在这一段，我将向你介绍 yay 中包含的那些 pacman 不包括的 pacman <operation>

#### [](#S "-S")`-S`[](#S)

##### [](#S-Si-Sl-Ss-Su-Sc-Qu "-S, -Si, -Sl, -Ss, -Su, -Sc, -Qu")`-S, -Si, -Sl, -Ss, -Su, -Sc, -Qu`[](#S-Si-Sl-Ss-Su-Sc-Qu)

这些操作 pacman 都支持，而与 pacman 不同的是，yay 的这些操作可以涵盖到**官方源 / 第三方源和 AUR** 中的所有包。

#### [](#Sc "-Sc")`-Sc`[](#Sc)

yay 将会清除 AUR 包构建时的缓存和没有被 track 的文件。没有被 track 的文件在这里指 AUR 包构建时下载的 sources 或者构建完成的 pkg 包，但是 vcs sources 会被保留（比如.`git`文件夹）

#### [](#全局的-options "全局的[options]")全局的 [options][](#全局的-options)

全局是指在所有 <operation> 下都可以加啦。

##### [](#repo "--repo")`--repo`[](#repo)

假定你给出的包名只存在源里（忽视 AUR 的存在）

##### [](#a-aur "-a(--aur)")`-a(--aur)`[](#a-aur)

假定你给出的包名只存在 AUR 中（忽视源的存在）

[](#配置设置 "配置设置")配置设置[](#配置设置)
-----------------------------

原版的 man 手册排的比较混乱，我这里自己细分了几个类型，或许不是特别专业，但我希望能够帮助你们理解。

### [](#自定义调用命令型 "自定义调用命令型")自定义调用命令型[](#自定义调用命令型)

##### [](#editor-lt-command-gt "--editor <command>")`--editor <command>`[](#editor-lt-command-gt)

设置编辑时调用的编辑器。

##### [](#makepkg-lt-command-gt "--makepkg <command>")`--makepkg <command>`[](#makepkg-lt-command-gt)

设置 makepkg 时需要调用 makepkg 命令（一般情况下用不到）

##### [](#pacman-lt-command-gt "--pacman <command>")`--pacman <command>`[](#pacman-lt-command-gt)

设置运行 pacman 时需要调用 pacman 命令（一般情况下用不到）

##### [](#tar-lt-command-gt "--tar <command>")`--tar <command>`[](#tar-lt-command-gt)

设置 makepkg 解压 tar 资源时调用的 tar 命令（一般情况下用不到）

##### [](#git-lt-command-gt "--git <command>")`--git <command>`[](#git-lt-command-gt)

设置 makepkg clone git 资源时调用的 git 命令（比如你可以安装 AUR 中的 fgit-go，使用`--git fgit`参数来让 fastgit 代理 clone 的过程）

##### [](#gpg-lt-command-gt "--gpg <command>")`--gpg <command>`[](#gpg-lt-command-gt)

设置 gpg 验证资源时调用的 gpg 命令

##### [](#sudo-lt-command-gt "--sudo <command>")`--sudo <command>`[](#sudo-lt-command-gt)

设置调用 sudo 获取 su 权限安装 pkg 时所调用的 sudo 命令。

### [](#自定义配置文件型 "自定义配置文件型")自定义配置文件型[](#自定义配置文件型)

##### [](#config-lt-file-gt "--config <file>")`--config <file>`[](#config-lt-file-gt)

设置读取的 pacman 配置文件。

##### [](#makepkgconf-lt-file-gt "--makepkgconf <file>")`--makepkgconf <file>`[](#makepkgconf-lt-file-gt)

设置读取的 makepkg 配置文件。

##### [](#nomakepkgconf "--nomakepkgconf")`--nomakepkgconf`[](#nomakepkgconf)

不读取系统中的 makepkg.conf，仅使用 Arch 默认状态下的配置文件。

### [](#自定义路径类型 "自定义路径类型")自定义路径类型[](#自定义路径类型)

##### [](#builddir-lt-dir-gt "--builddir <dir>")`--builddir <dir>`[](#builddir-lt-dir-gt)

设置 build 路径，默认路径为`~/.cache/yay/`

##### [](#absdir-lt-dir-gt "--absdir <dir>")`--absdir <dir>`[](#absdir-lt-dir-gt)

设置 abs 路径，默认路径为`~/.cache/yay/abs/`

### [](#参数传递型 "参数传递型")参数传递型[](#参数传递型)

##### [](#editorflags-lt-flags-gt "--editorflags <flags>")`--editorflags <flags>`[](#editorflags-lt-flags-gt)

后跟需要跟随传递给编辑器的参数。如果需要传递多个参数，可以使用引号。

##### [](#mflags-lt-flags-gt "--mflags <flags>")`--mflags <flags>`[](#mflags-lt-flags-gt)

后跟需要跟随传递给 makepkg 的参数。如果需要传递多个参数，可以使用引号。

这个用的人不多，但其实是非常好用的一个功能。在我们安装`deepin-wine-tim`等包的时候，很可能会遇到文件明明完整但 checksum 不通过的情况，这时我们可以跟一个`--skipchecksums`参数传递给 makepkg 以跳过 checksum 的过程。

##### [](#gpgflags-lt-flags-gt "--gpgflags <flags>")`--gpgflags <flags>`[](#gpgflags-lt-flags-gt)

后跟需要跟随传递给 pgp 的参数。如果需要传递多个参数，可以使用引号。

##### [](#sudoflags-lt-flags-gt "--sudoflags <flags>")`--sudoflags <flags>`[](#sudoflags-lt-flags-gt)

后跟需要跟随传递给 sudo 的参数。如果需要传递多个参数，可以使用引号。

### [](#菜单配置型 "菜单配置型")菜单配置型[](#菜单配置型)

#### [](#clean菜单 "clean菜单")clean 菜单[](#clean菜单)

启用清除询问菜单。（询问你是否需要清除已存在的文件）

禁用清除询问菜单。（不询问你是否需要清除已存在的文件）

##### [](#answerclean "--answerclean")`--answerclean`[](#answerclean)

自动回答 cleanmenu，后跟`<All|None|Installed|NotInstalled>`参数。

##### [](#noanswerclean "*--noanswerclean")*`--noanswerclean`[](#noanswerclean)

不设置自动回答。

#### [](#diff菜单 "diff菜单")diff 菜单[](#diff菜单)

启用对比询问菜单。（询问你是否需要对比本地文件和 AUR 文件）

禁用对比询问菜单。（不询问你是否需要对比本地文件和 AUR 文件）

##### [](#answerdiff "--answerdiff")`--answerdiff`[](#answerdiff)

自动回答 cleanmenu，后跟`<All|None|Installed|NotInstalled>`参数。

##### [](#noanswerdiff "*--noanswerdiff")*`--noanswerdiff`[](#noanswerdiff)

不设置自动回答。

#### [](#edit菜单 "edit菜单")edit 菜单[](#edit菜单)

启用修改询问菜单。（询问你是否需要修改 PKGBUILD 以及相关文件）

禁用修改询问菜单。（不询问你是否需要修改 PKGBUILD 以及相关文件）

##### [](#answeredit "--answeredit")`--answeredit`[](#answeredit)

自动回答 editmenu，后跟`<All|None|Installed|NotInstalled>`参数。

##### [](#noansweredit "*--noansweredit")*`--noansweredit`[](#noansweredit)

不设置自动回答。

#### [](#upgrade菜单 "upgrade菜单")upgrade 菜单[](#upgrade菜单)

启用更新询问菜单。（询问你是否需要更新 AUR 包）

禁用更新询问菜单。（不询问你是否需要更新 AUR 包）

##### [](#answerupgrade "--answerupgrade")`--answerupgrade`[](#answerupgrade)

自动回答 upgrademenu，后跟`<All|None|Installed|NotInstalled`参数。

##### [](#noanswerupgrade "*--noanswerupgrade")*`--noanswerupgrade`[](#noanswerupgrade)

不设置自动回答。

#### [](#removemake菜单 "removemake菜单")removemake 菜单[](#removemake菜单)

##### [](#askremovemake "*--askremovemake")*`--askremovemake`[](#askremovemake)

在编译结束后，询问是否删除 make depend。

##### [](#removemake "--removemake")`--removemake`[](#removemake)

在编译结束后，删除 make depend。

##### [](#noremovemake "--noremovemake")`--noremovemake`[](#noremovemake)

在编译结束后，不删除 make depend。

#### [](#provides菜单 "provides菜单")provides 菜单[](#provides菜单)

##### [](#provides "*--provides")*`--provides`[](#provides)

搜索 AUR 包时，一同寻找其在 AUR 上的依赖程序。 当找到多个提供该依赖的包时，将出现一个菜单，提示您选择一个。尽管这不会引起注意，但这会增加依赖项解决时间。

##### [](#noprovides "--noprovides")`--noprovides`[](#noprovides)

搜索 AUR 包时，不在 AUR 上寻找其依赖程序。尽管 yay 不会再次弹出依赖菜单供你选择，yay 调用 pacman 时依然会出现 pacman 的选择菜单让你选择。

#### [](#pgpfetch菜单 "pgpfetch菜单")pgpfetch 菜单[](#pgpfetch菜单)

##### [](#pgpfetch "*--pgpfetch")*`--pgpfetch`[](#pgpfetch)

询问你是否从每个 PKGBUILD 的 validpgpkeys 字段导入未知的 PGP 密钥。

##### [](#nopgpfetch "--nopgpfetch")`--nopgpfetch`[](#nopgpfetch)

不自动导入陌生的 PGP 密钥。

#### [](#useask选项 "useask选项")useask 选项[](#useask选项)

##### [](#useask "*--useask")*`--useask`[](#useask)

调用 pacman 的–ask 询问用户是否删除系统中与当前包冲突的软件包。

##### [](#nouseask "--nouseask")`--nouseask`[](#nouseask)

不调用 pacman 的–ask 询问用户是否删除系统中与当前包冲突的软件包，遇到冲突的软件包时直接报错，由用户来手动解决。

#### [](#combinedupgrade菜单 "combinedupgrade菜单")combinedupgrade 菜单[](#combinedupgrade菜单)

##### [](#combinedupgrade "--combinedupgrade")`--combinedupgrade`[](#combinedupgrade)

在系统更新期间，将源内包和 AUR 包的更新菜单合并到一起。

##### [](#nocombinedupgrade "*--nocombinedupgrade")*`--nocombinedupgrade`[](#nocombinedupgrade)

在系统更新期间，先支持源内包的升级，完成后再进行 AUR 包的升级。

### [](#T-or-F-型 "T or F 型")T or F 型[](#T-or-F-型)

#### [](#devel "devel")devel[](#devel)

##### [](#devel-1 "--devel")`--devel`[](#devel-1)

在系统更新期间，检查 AUR 的 vcs 包是否有更新，当前仅支持 AUR 的 - git 包。 devel 查询是使用`git ls-remote`对比安装时和现在最新的 commit_id 完成的。

##### [](#nodevel "*--nodevel")*`--nodevel`[](#nodevel)

在系统更新期间， 不检查 AUR 的 vcs 包是否有更新。

#### [](#timeupdate "timeupdate")timeupdate[](#timeupdate)

##### [](#timeupdate-1 "--timeupdate")`--timeupdate`[](#timeupdate-1)

在系统更新期间，将已安装软件包的构建时间与每个软件包的 AUR 的最后修改时间进行比较。

##### [](#notimeupdate "*--notimeupdate")*`--notimeupdate`[](#notimeupdate)

在系统更新期间，不将已安装软件包的构建时间与每个软件包的 AUR 的最后修改时间进行比较。

#### [](#redownload "redownload")redownload[](#redownload)

##### [](#redownload-1 "--redownload")`--redownload`[](#redownload-1)

就算 PKGBUILD 已经存在，也要重新从 AUR 上获取一份新的 PKGBUILD 并覆盖原有 PKGBUILD。

##### [](#redownloadall "--redownloadall")`--redownloadall`[](#redownloadall)

就算 PKGBUILD 已经存在，也要重新从 AUR 上获取所有 AUR 包的 PKGBUILD 并覆盖原有 PKGBUILD。

##### [](#noredownload "*--noredownload")*`--noredownload`[](#noredownload)

当下载 PKGBUILD 时，，如果发现 cache 中的 PKGBUILD 版本＞＝AUR 上的版本时，直接使用本地的 PKGBUILD。

#### [](#rebuild "rebuild")rebuild[](#rebuild)

##### [](#rebuild-1 "--rebuild")`--rebuild`[](#rebuild-1)

即使在 cache 中有可用的二进制包的情况下，也始终要重新编译目标软件包。

##### [](#rebuildall "--rebuildall")`--rebuildall`[](#rebuildall)

即使在 cache 中有可用的二进制包的情况下，也始终要重新编译所有的 AUR 包。

##### [](#rebuildtree "--rebuildtree")`--rebuildtree`[](#rebuildtree)

安装 AUR 包时，以递归方式重新编译并重新安装其所有 AUR 依赖包，即使已安装的依赖项也是如此。 该选项使您可以轻松地针对当前系统的库重新构建软件包，如果它们变得不兼容。（比如 python3.8->3.9）

##### [](#norebuild "*--norebuild")*`--norebuild`[](#norebuild)

构建软件包时，如果在缓存中找到该软件包并且该软件包与想要的软件包的版本相同，则跳过软件包的编译过程并使用现有的二进制程序。

#### [](#sudoloop "sudoloop")sudoloop[](#sudoloop)

##### [](#sudoloop-1 "--sudoloop")`--sudoloop`[](#sudoloop-1)

在后台循环调用 sudo，以防止 sudo 授权在长时间构建期间超时。

##### [](#nosudoloop "*--nosudoloop")*`--nosudoloop`[](#nosudoloop)

不在后台循环调用 sudo，可能会导致 sudo 授权在长时间构建期间超时。

#### [](#batchinstall "batchinstall")batchinstall[](#batchinstall)

##### [](#batchinstall-1 "--batchinstall")`--batchinstall`[](#batchinstall-1)

在构建和安装 AUR 包时，对每个软件包的安装进行排序，而并非在构建之后立刻安装每个软件包时。 需要注意的是，一旦构建了所有软件包，或者需要构建队列中的软件包作为构建另一个软件包的依赖项，应当在安装队列中安装所有软件包。

##### [](#nobatchinstall "*--nobatchinstall")*`--nobatchinstall`[](#nobatchinstall)

在构建 AUR 包成功后立即安装。

#### [](#clearafter "clearafter")clearafter[](#clearafter)

##### [](#cleanafter "--cleanafter")`--cleanafter`[](#cleanafter)

在构建 AUR 包完成以后清除 cache 文件。

##### [](#nocleanafter "*--nocleanafter")*`--nocleanafter`[](#nocleanafter)

在构建 AUR 包完成以后不清除 cache 文件。

### [](#其他型 "其他型")其他型[](#其他型)

##### [](#save "--save")`--save`[](#save)

把你这一次执行 yay 后面跟的配置参数永久保存下来。

##### [](#aururl "--aururl")`--aururl`[](#aururl)

更改 aur 源地址（默认为 [https://aur.archlinux.org](https://aur.archlinux.org/) ），~适用于中国用户，可以使用此参数将 AUR 的地址设置成清华的反代，具体的配置命令为~

```
yay --aururl "https://aur.tuna.tsinghua.edu.cn" --save
```

TUNA 的反代已经取消，可以使用如下命令设置回 AUR 官方源

```
yay --aururl "https://aur.archlinux.org" --save
```

##### [](#sortby "--sortby")`--sortby`[](#sortby)

在搜索过程中，按特定条件对 AUR 结果进行排序，后跟`<votes|popularity|id|baseid|name|base|submitted|modified>`参数，默认为`votes`。

##### [](#searchby "--searchby")`--searchby`[](#searchby)

通过指定查询类型来搜索 AUR 软件包，后跟`<name|name-desc|maintainer|depends|checkdepends|makedepends|optdepends>`参数，默认为`name-desc`。

##### [](#topdown "*--topdown")*`--topdown`[](#topdown)

优先展示源内包，其次才是 AUR 包

##### [](#bottomup "--bottomup")`--bottomup`[](#bottomup)

优先展示 AUR 包，其次才是源内包

##### [](#requestsplitn-lt-number-gt "--requestsplitn <number>")`--requestsplitn <number>`[](#requestsplitn-lt-number-gt)

设置在每次向 AUR 的请求的最大数值（默认 150）。数值越高，请求时间越短，但是单次请求的数值过大会导致 error。当这个数值＞500 时你应当特别注意这一点。

##### [](#completioninterval-lt-days-gt "--completioninterval <days>")`--completioninterval <days>`[](#completioninterval-lt-days-gt)

刷新完成高速缓存的时间（以天为单位, 默认为 7）。 将此值设置为 0 将导致每次刷新缓存，而将其设置为 - 1 将导致永远不刷新缓存。

[](#我个人的常用命令 "我个人的常用命令")我个人的常用命令[](#我个人的常用命令)
---------------------------------------------

```
yay
yay foo
yay -Sa foo
yay -Scc
yay -Ps
yay -Pww
yay -Gpa
yay -Ga
```

_本文同时发布于「[知乎专栏](https://zhuanlan.zhihu.com/p/363666022)」，如果你恰好有知乎帐号的话或许可以考虑帮我点个赞？_