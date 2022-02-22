> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [wiki.archlinux.org](https://wiki.archlinux.org/title/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Tips_and_tricks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

> Pacman 本身也是 bash 程序，所以有些通用优化请参考 Core utilities 和 Bash.

Pacman 本身也是 bash 程序，所以有些通用优化请参考 [Core utilities](https://wiki.archlinux.org/title/Core_utilities "Core utilities") 和 [Bash](https://wiki.archlinux.org/title/Bash "Bash").

维护
--

保持系统干净，遵循 [Arch 之道](https://wiki.archlinux.org/title/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")。参考 [System maintenance](https://wiki.archlinux.org/title/System_maintenance "System maintenance").

### 查询软件包

要获取已经安装的软件包以及它们的版本：

*   所有明确安装的软件包: `pacman -Qe`.
*   列出 `_group_` [软件包组](https://wiki.archlinux.org/title/Package_group "Package group") 中的所有软件包: `pacman -Sg _group_`
*   所有明确安装的，存在于数据库而且不是直接或可选依赖的软件包: `pacman -Qent`.
*   所有外部软件包 (通常是手动下载安装，或者已经从数据库中删除): `pacman -Qm`.
*   所有从数据库中安装的软件包: `pacman -Qn`.
*   按正则表达式查询软件包: `pacman -Qs _regex_`.
*   按正则表达式查询软件包，自定义输出格式：`expac -s "%-30n %v" _regex_` (需要安装 [显示所有软件包及其大小
    
    将所有软件包按占用空间大小排序输出：
    
    ](https://archlinux.org/packages/?>expac</a>).</li></ul>
    <h3 id=)
    
    [](https://archlinux.org/packages/?>expac</a>).</li></ul>
    <h3 id=)*   [安装](https://archlinux.org/packages/?>expac</a>).</li></ul>
        <h3 id=)[](https://archlinux.org/packages/?>expac</a> 并运行 <code> expac -s )
    [](https://archlinux.org/packages/?>expac</a> 并运行 <code> expac -s )*   [用 [community] 中的](https://archlinux.org/packages/?>expac</a> 并运行 <code> expac -s ) [获取大小
        
        用下面命令查看单个软件包的大小:
        
        ```
        $ LC_ALL=C pacman -Qi | awk '/^Name/{name=$3} /^Installed Size/{print $4$5, name}' | sort -h
        
        
        ```
        
        用下面命令按大小排序安装的软件包及其依赖的大小:
        
        ](https://archlinux.org/packages/?>pacgraph</a> 加 -c 选项可以生成所有安装的软件包及其大小.</li></ul>
        <h4 id=)
        
        [](https://archlinux.org/packages/?>pacgraph</a> 加 -c 选项可以生成所有安装的软件包及其大小.</li></ul>
        <h4 id=)*   [安装](https://archlinux.org/packages/?>pacgraph</a> 加 -c 选项可以生成所有安装的软件包及其大小.</li></ul>
            <h4 id=) [base-devel](https://archlinux.org/packages/?>expac</a> 并运行 <code>expac -H M '%m\t%n' | sort -h</code>.</li>
            <li>以 <code>-c</code> 参数执行 <a rel=) 的软件包，带大小和描述：
            
            ```
            $ expac -H M "%011m\t%-20n\t%10d" $(comm -23 <(pacman -Qqen | sort) <(pacman -Qqg base base-devel | sort)) | sort -n
            
            
            ```
            
            #### 按日期查询
            
            用 [查找不属于任何软件包的文件](https://archlinux.org/packages/?>expac</a> 查询最近安装的 20 个软件包：
            </p>
            <pre>$ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20
            
            </pre>
            <p>用从 epoch(1970-01-01 UTC) 开始的秒数：
            </p>
            <pre>$ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20
            
            </pre>
            <h4 id=)
            
            [建议定期检查 pacman 数据库之外的文件。通常这些文件是第三方程序使用一般方式安装 (例如 **./configure; make; make install**)。下面脚本可以找出它们：](https://archlinux.org/packages/?>expac</a> 查询最近安装的 20 个软件包：
            </p>
            <pre>$ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20
            
            </pre>
            <p>用从 epoch(1970-01-01 UTC) 开始的秒数：
            </p>
            <pre>$ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20
            
            </pre>
            <h4 id=)
            
            [
            
            ```
            pacman-disowned
            
            ```
            
            ```
            #!/bin/sh
            
            tmp=${TMPDIR-/tmp}/pacman-disowned-$UID-$$
            db=$tmp/db
            fs=$tmp/fs
            
            mkdir "$tmp"
            trap  'rm -rf "$tmp"' EXIT
            
            pacman -Qlq | sort -u > "$db"
            
            find /bin /etc /lib /sbin /usr \
              ! -name lost+found \
              \( -type d -printf '%p/\n' -o -print \) | sort > "$fs"
            
            comm -23 "$fs" "$db"
            
            
            ```
            
            要生成列表：
            
            ```
            $ pacman-disowned > non-db.txt
            
            
            ```
            
            注意删除 `non-db.txt` 中的文件时先仔细确认。有些是配置文件、日志等，不要删除它们。
            
            ### 删除孤立软件包
            
            递归删除孤立软件包：
            
            ```
            # pacman -Qtdq | pacman -Rns -
            
            
            ```
            
            如果没有孤立软件包，将显示错误 `error: argument '-' specified with empty stdin`. 这个是正常的，因为 `pacman -Rns` 没有收到任何参数.
            
            **注意：** `-Qt` 仅显示真的孤立包，要包含可选依赖，请使用 `-Qtt` .
            
            ### 删除必须的软件包以外的所有软件包
            
            先将明确安装的软件包改为依赖关系:
            
            ```
            # pacman -D --asdeps $(pacman -Qqe)
            
            
            ```
            
            然后将需要保留的软件包设置为明确安装:
            
            ```
            # pacman -D --asexplicit base linux linux-firmware
            
            
            ```
            
            然后删除所有没有明确安装的软件包.
            
            ### 仅显示正式安装的软件包
            
            ```
            pacman -Qq |grep -Fv -f <(pacman -Qqm)
            
            
            ```
            
            安装和修复
            -----
            
            几种获取和修复软件包的方法。
            
            ### 从 CD/DVD/ISO 安装软件包
            
            *   先挂载 CD （如果需要，替换_cdrom_为_dvd_或其他介质)：
            
            ```
            # mount /mnt/cdrom
            
            
            ```
            
            如果使用的是 ISO 映像，先在 /mnt 建立一个目录：
            
            ```
            # mkdir /mnt/iso
            
            
            ```
            
            然后挂载镜像：
            
            ```
            # mount -t iso9660 -o ro,loop /path/to/iso /mnt/iso
            
            
            ```
            
            *   配置 pacman：
            
            ```
            # nano -w /etc/pacman.conf
            
            
            ```
            
            *   将如下仓库信息添加到其他软件仓库（如 extra、core）之前，确保优先使用介质中的软件包：
            
            ```
            # 使用 cdrom 作为仓库
            [custom]
            Server = file:///mnt/cdrom/arch/pkg
            
            
            ```
            
            如果使用其他介质，记得替换 _cdrom_ 。
            
            修改`pacman.conf`后，更新软件仓库即可。
            
            #### 从 Arch 的 core 镜像安装软件包
            
            如果暂时无法链接网络（比如要配置无线网络），可以通过 Arch 的 core 仓库镜像获取软件包。先挂载之：
            
            ```
            # mount -o loop /path/to/arch_core_image/i686/repo-core-i686.sfs /mnt/iso
            
            
            ```
            
            然后修改`pacman.conf`的`[core]`段，（临时）替换为镜像挂载的位置：
            
            ```
            [core]
            #Include = /etc/pacman.d/mirrorlist
            Server = file:///mnt/iso
            
            
            ```
            
            然后同步：
            
            ```
            # pacman -Syu
            
            
            ```
            
            ### 自建本地仓库
            
            pacman 3 引入了一个名为`repo-add`脚本，用于帮助个人用户生成软件仓库。使用 `repo-add --help` 查看详细用法。
            
            将所有要加入仓库的软件包放入一个目录，运行如下命令（_repo_是自建仓库的名称）：
            
            ```
            $ repo-add /path/to/repo.db.tar.gz /path/to/*.pkg.tar.xz
            
            
            ```
            
            注意，`repo-add`生成的数据库文件不一定和软件包放在同一目录，但使用 pacman 同步时，两者必须放在一起。
            
            向仓库添加新软件包（并移除旧的）：
            
            ```
            $ repo-add /path/to/repo.db.tar.gz /path/to/packagetoadd-1.0-1-i686.pkg.tar.xz
            
            
            ```
            
            **注意：** 使用`repo-remove`删除软件包。
            
            ](https://archlinux.org/packages/?>expac</a> 查询最近安装的 20 个软件包：
            </p>
            <pre>$ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20
            
            </pre>
            <p>用从 epoch(1970-01-01 UTC) 开始的秒数：
            </p>
            <pre>$ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20
            
            </pre>
            <h4 id=)
            
            [本地仓库建立后，添加仓库到`pacman.conf`。`db.tar.gz`文件的名字就是仓库的名字，路径格式是_file://..._或 FTP 地址](https://archlinux.org/packages/?>expac</a> 查询最近安装的 20 个软件包：
            </p>
            <pre>$ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20
            
            </pre>
            <p>用从 epoch(1970-01-01 UTC) 开始的秒数：
            </p>
            <pre>$ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20
            
            </pre>
            <h4 id=)_[ftp://localhost/path/to/directory](ftp://localhost/path/to/directory)_。
            
            欢迎到[非官方用户软件仓库](https://wiki.archlinux.org/title/Unofficial_user_repositories "Unofficial user repositories")，分享你的仓库。
            
            ### 在网络上共享 pacman 缓存
            
            要在多机间共享软件包，使用任何网络协议共享`/var/cache/pacman/`目录即可。本节介绍如何使用 shfs 或 sshfs，在局域网内的多机间分享软件包及相关库文件目录。注意，网络间共享可能速度缓慢，取决于所选文件系统等因素。
            
            首先，在服务器安装任意网络文件系统：[SSHFS](https://wiki.archlinux.org/title/SSHFS "SSHFS")，[shfs](https://wiki.archlinux.org/title/Shfs "Shfs")，[ftpfs](https://wiki.archlinux.org/index.php?title=Ftpfs&action=edit&redlink=1 "Ftpfs (page does not exist)")，[smbfs](https://wiki.archlinux.org/title/Smbfs "Smbfs") 或 [NFS](https://wiki.archlinux.org/title/NFS "NFS")。
            
            然后，挂载服务器的`/var/cache/pacman/pkg`到客户端机器上的`/var/cache/pacman/pkg`目录即可。
            
            要分享软件包数据，使用同样方法共享`/var/lib/pacman/sync/{core,extra,testing,community}`即可。修改`/etc/fstab`以开机自动挂载。
            
            #### 避免过度清理缓存
            
            执行`pacman -Sc`清理软件包缓存时，会删除所有当前机器上未安装的软件包。由于 pacman 无法判断软件包是否在其他机器上安装，这会导致移除某些还需要的软件包。
            
            避免的方法是修改清理方式为：删除所有已有新版本的过期软件包。添加以下内容到`/etc/pacman.conf`的`[options]`段：
            
            ```
            CleanMethod = KeepCurrent
            
            
            ```
            
            ### 备份和恢复已安装软件包
            
            定期备份软件包是个好习惯。万一系统出了大问题，需要重装，就可以利用备份的软件包恢复到原先的系统。
            
            *   第一步，生成系统上安装的非本地（即从官方仓库获取的）软件包列表：
            
            ```
             $ comm -23 <(pacman -Qeq|sort) <(pacman -Qmq|sort) > pkglist
            
            
            ```
            
            *   把生成的 pkglist 存储在一个安全的地方，比如 U 盘，或者 gist.github.com、evernote、dropbox 之类的文本储存网站。
            
            *   今后重装系统时，把 pkglist 复制到新系统。
            
            *   使用如下命令安装所有软件包：
            
            ```
             # pacman -S $(< pkglist)
            
            
            ```
            
            要是备份的软件包列表包含非官方软件包（从 AUR 或其他什么地方下载的），就得使用下面这个吓人的命令了，不然 pacman 会出错：
            
            ```
            # pacman -S --needed $(diff <(cat badpkglist|sort) <(diff <(cat badpkglist|sort) <(pacman -Slq|sort)|grep \<|cut -f2 -d' ')|grep \<|cut -f2 -d' ')
            
            
            ```
            
            解释：
            
            *   _pacman -Slq_列出所有可以安装的软件包。由于输出是按照来源仓库排序的，需要再调用_sort_排序。
            *   排序是为_diff_命令比对列表做准备。
            *   第一个_diff_返回所有无法安装的软件包；第二个返回所有可以安装的软件包。
            *   _--needed_表示跳过已安装软件包。
            
            可以接着用_yaourt_恢复从 AUR 获取的软件包（不推荐）：
            
            ```
            $ yaourt -S --noconfirm $(diff <(cat badpkglist|sort) <(pacman -Slq|sort) |grep \<|cut -f2 -d' ')
            
            
            ```
            
            最后，还可以卸载掉新系统上安装的、但之前系统并未安装的软件包。 警告：务必小心使用，仔细查看 pacman 输出，避免悲剧。
            
            ```
            # pacman -Rsu $(diff <(cat badpkglist|sort) <(pacman -Qq|sort) | grep \>|cut -f2 -d' ')
            
            
            ```
            
            ### 列出所有不属于 base 或 base-devel 的已安装软件包
            
            下列命令输出所有不属于 base 或 base-devel 软件包组的已安装软件包。这些软件包一般都是用户自己安装的：
            
            ```
            comm -23 <(pacman -Qeq|sort) <(pacman -Qgq base base-devel|sort)
            
            
            ```
            
            ### 重新安装所有软件包
            
            要是你的系统遭到了大规模破坏（比如`rm -rf`什么的），可以通过 pacman 重新安装所有软件包来挽救。
            
            如果没有安装来自软件源外的软件包（比如来自 AUR 的），使用如下命令即可：
            
            ```
            # pacman -Qqn | pacman -S -
            # pacman -S $(pacman -Qqn) # 如果上面的命令无法输入 y 以确认安装
            
            
            ```
            
            如果安装了外来软件包，你可以使用 `pacman -Qqm` 列出它们
            
            ### 从已有安装修复 USB 系统
            
            如果你有一个 Arch 安装在 U 盘上，不小心搞坏了（比如，写入 U 盘时断电了），可以使用主机上的 Arch 修复 U 盘上的 Arch（假设 U 盘挂载在 / newarch）：
            
            ```
            # pacman -S $(pacman -Qq --dbpath /newarch/var/lib/pacman) --root /newarch --dbpath /newarch/var/lib/pacman
            
            
            ```
            
            ### 解压缩软件包
            
            Arch 软件包其实就是普通的 xz 压缩包，解压方法没啥特别的：
            
            ```
            $ tar -Jxvf package.tar.xz
            
            
            ```
            
            性能
            --
            
            ### 加快下载速度
            
            **注意：** 如果你的包下载速度变得极慢，首先确定你用的是那些 ([镜像](https://wiki.archlinux.org/title/Mirrors_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mirrors (简体中文)")) 网站而不是 ftp.archlinux.org，因为后者[从 2007 年 3 月开始限速](https://archlinux.org/news/302/)。
            
            可以通过各种下载工具而不是 Pacman 内置的下载方式，来改善 Pacman 的下载速度。
            
            不论怎样，在做任何修改前，你必须确定拥有了最新版的 Pacman：
            
            ```
            # pacman -Syu
            
            
            ```
            
            #### 使用 Powerpill
            
            Powerpill 是 Pacman 的完整包裹程序，增加了平行下载和分段下载功能，加速下载过程。Pacman 一次只下载一个软件包，完成后才开始下一个下载。 Powerpill 同时下载多个软件包。[Powerpill wiki 页面](https://wiki.archlinux.org/title/Powerpill "Powerpill")提供了基本的配置和使用方法。
            
            #### 使用 wget
            
            对于需要更强大代理支持的用户来说，用 wget 比用 Pacman 自己的下载方式更加方便。
            
            要使用 `wget`，首先使用`pacman -S wget`安装它，然后修改`/etc/pacman.conf`并在其中的`[options]`区段将下面内容去掉注释：
            
            ```
            XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u
            
            ```
            
            除了将`wget`参数放在`/etc/pacman.conf`里，你也可以直接修改`wget`配置文件（全局文件是`/etc/wgetrc`，各个用户的文件是`$HOME/.wgetrc`）。
            
            ### 使用 aria2
            
            [aria2](https://wiki.archlinux.org/title/Aria2 "Aria2") 是一个具有断点续传和分块下载功能的轻量级下载软件，支持 HTTP/HTTPS/FTP 协议。[aria2](http://aria2.sourceforge.net/) 可以多线程通过 HTTP/HTTPS 和 FTP 协议连接镜像服务器，显著提高下载速度。
            
            **注意：** 在 Pacman 的 XferCommand 使用 aria2c **不会**导致并行下载多个包。因为 Pacman 调用 XferCommand 时是一次一个包调用的，等待下载完成才会启动下一个。想要并行下载多个包，参见上面的 [powerpill-light](#使用_Powerpill) 部分。
            
            #### 安装
            
            通过`pacman -S aria2`安装 [配置](https://archlinux.org/packages/?>aria2</a>。
            </p>
            <h4 id=)
            
            [修改`/etc/pacman.conf`，在`[option]`段添加下列一行（如果已存在则修改之）：](https://archlinux.org/packages/?>aria2</a>。
            </p>
            <h4 id=)
            
            [
            
            ```
            XferCommand = /usr/bin/aria2c --allow-overwrite=true -c --file-allocation=none --log-level=error -m2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 -t5 -d / -o %o %u
            
            ```
            
            #### 参数细节
            
            ](https://archlinux.org/packages/?>aria2</a>。
            </p>
            <h4 id=)
            
            [
            
            `/usr/bin/aria2c`
            
            aria2 主程序的完整路径。
            
            `--allow-overwrite=true`
            
            如果相应的控制文件不存在则重新下载。(默认值：false)
            
            `-c, --continue`
            
            如果相应的控制文件存在则继续未完成的下载。
            
            `--file-allocation=none`
            
            下载开始前预设空间。(默认值: prealloc) **1**
            
            `--log-level=error`
            
            设置错误输出级别。 (默认值: debug)
            
            `-m2, --max-tries=2`
            
            从每个镜像源下载特定文件的最大尝试次数设为 2。 (默认值: 5)
            
            `--max-connection-per-server=2`
            
            下载每个文件时到每个镜像源的最大连接数设为 2。(默认值: 1)
            
            `--max-file-not-found=5`
            
            如果 5 次尝试后仍未下载完成 1 字节则强制停止。(默认值: 0)
            
            `--min-split-size=5M`
            
            只有当文件大于 5MB 时才分割下载。 (默认值: 20M)
            
            `--no-conf`
            
            不加载 `aria2.conf` 。 (默认值: `~/.aria2/aria2.conf`)
            
            `--remote-time=true`
            
            对远程文件应用时间戳并应用到本地文件。 (默认值: false)
            
            `--summary-interval=60`
            
            每 60s 显式一次下载总进度。 (默认值: 60) **2**
            
            `-t5, --timeout=5`
            
            对镜像源的连接建立后 5s 超时。 (默认值: 60)
            
            `-d, --dir`
            
            ](https://archlinux.org/packages/?>aria2</a>。
            </p>
            <h4 id=)
            
            [由](https://archlinux.org/packages/?>aria2</a>。
            </p>
            <h4 id=) [pacman](https://wiki.archlinux.org/title/Pacman "Pacman") 设定的文件下载目录。
            
            `-o, --output`
            
            输出的下载文件的文件名
            
            `%o`
            
            代表 pacman 指定的文件名的变量
            
            `%u`
            
            代表 pacman 指定的 URL 的变量
            
            ##### 其他解释
            
            1 `--file-allocation=falloc`
            
            对较新的文件系统建议使用，如 ext4(支持 extents)、 btrfs 和 xfs 因为它们存储大文件 (GB 级别) 时速度很快。 较老的文件系统如 ext3 则不要使用 falloc，因为 prealloc 消耗的时间几乎和标准分配相同，同时会锁定 aria2 进程而停止下载。
            
            2 `--summary-interval=0`
            
            减少下载总进度的输出并有可能改善性能。日志会按照 `log-level` 选项的设置继续输出。
            
            #### 使用其它程序
            
            这里还有一些可以和 Pacman 协同工作的下载软件。下面列举了它们对应的 XferCommand 命令写法：
            
            *   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
            *   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
            *   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`
            
            工具
            --
            
            *   **Lostfiles** — Script that identifies files not owned by any package.
            
            [https://github.com/graysky2/lostfiles](https://github.com/graysky2/lostfiles) || [http://kmkeen.com/pacmatic](https://archlinux.org/packages/?>lostfiles</a></dd></dl>
            <ul><li><b>Pacmatic</b> — <i>Pacman</i> wrapper to check Arch News before upgrading, avoid partial upgrades, and warn about configuration file changes.</li></ul>
            <dl><dd><a rel=) || [https://github.com/andrewgregory/pacutils](https://archlinux.org/packages/?>pacmatic</a></dd></dl>
            <ul><li><b>pacutils</b> — Helper library for libalpm based programs.</li></ul>
            <dl><dd><a rel=) || [pkgfile](https://archlinux.org/packages/?>pacutils</a></dd></dl>
            <ul><li><b><a href=) — Tool that finds what package owns a file.
            
        
        [https://github.com/falconindy/pkgfile](https://github.com/falconindy/pkgfile) || [https://github.com/Daenyth/pkgtools](https://archlinux.org/packages/?>pkgfile</a></dd></dl>
        <ul><li><b>pkgtools</b> — Collection of scripts for Arch Linux packages.</li></ul>
        <dl><dd><a rel=) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)AUR
        
        *   **pkgtop** — Interactive package manager and resource monitor designed for the GNU/Linux.
        
        [https://github.com/orhun/pkgtop](https://github.com/orhun/pkgtop) || [pkgtop-git](https://aur.archlinux.org/packages/pkgtop-git/)AUR
        
        *   **[Powerpill](https://wiki.archlinux.org/title/Powerpill "Powerpill")** — Uses parallel and segmented downloading through [aria2](https://wiki.archlinux.org/title/Aria2 "Aria2") and [Reflector](https://wiki.archlinux.org/title/Reflector "Reflector") to try to speed up downloads for _pacman_.
        
        [https://xyne.dev/projects/powerpill/](https://xyne.dev/projects/powerpill/) || [powerpill](https://aur.archlinux.org/packages/powerpill/)AUR
        
        *   **repoctl** — Tool to help manage local repositories.
        
        [https://github.com/cassava/repoctl](https://github.com/cassava/repoctl) || [repoctl](https://aur.archlinux.org/packages/repoctl/)AUR
        
        *   **repose** — An Arch Linux repository building tool.
        
        [https://github.com/vodik/repose](https://github.com/vodik/repose) || [snap-pac](https://archlinux.org/packages/?>repose</a></dd></dl>
        <ul><li><b><a href=) — Make _pacman_ automatically use snapper to create pre/post snapshots like openSUSE's YaST.
        
    
    [https://github.com/wesbarnett/snap-pac](https://github.com/wesbarnett/snap-pac) || [https://github.com/orospakr/vrms-arch](https://archlinux.org/packages/?>snap-pac</a></dd></dl>
    <ul><li><b>vrms-arch</b> — A virtual Richard M. Stallman to tell you which non-free packages are installed.</li></ul>
    <dl><dd><a rel=) || [vrms-arch](https://aur.archlinux.org/packages/vrms-arch/)AUR
    
    ### 图形前端
    
    **警告：** PackageKit opens up system permissions by default, and is otherwise not recommended for general usage. See [FS#50459](https://bugs.archlinux.org/task/50459) and [FS#57943](https://bugs.archlinux.org/task/57943).
    
    *   **Apper** — Qt 5 application and package manager using PackageKit written in C++. Supports [AppStream metadata](https://www.freedesktop.org/wiki/Distributions/AppStream/).
    
    [https://userbase.kde.org/Apper](https://userbase.kde.org/Apper) || [AppStream metadata](https://archlinux.org/packages/?>apper</a></dd></dl>
    <ul><li><b>Discover</b> — Qt 5 application manager using PackageKit written in C++/QML. Supports <a rel=), [Flatpak](https://wiki.archlinux.org/title/Flatpak "Flatpak") and [firmware updates](https://wiki.archlinux.org/title/Fwupd "Fwupd").
    

[https://userbase.kde.org/Discover](https://userbase.kde.org/Discover) || [https://freedesktop.org/software/PackageKit/](https://archlinux.org/packages/?>discover</a></dd></dl>
<ul><li><b>GNOME PackageKit</b> — GTK 3 package manager using PackageKit written in C.</li></ul>
<dl><dd><a rel=) || [AppStream metadata](https://archlinux.org/packages/?>gnome-packagekit</a></dd></dl>
<ul><li><b>GNOME Software</b> — GTK 3 application manager using PackageKit written in C. Supports <a rel=), [Flatpak](https://wiki.archlinux.org/title/Flatpak "Flatpak") and [firmware updates](https://wiki.archlinux.org/title/Fwupd "Fwupd").

[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [https://github.com/schuay/pcurses](https://archlinux.org/packages/?>gnome-software</a></dd></dl>
<ul><li><b>pcurses</b> — Curses TUI pacman wrapper written in C++.</li></ul>
<dl><dd><a rel=) || [https://sourceforge.net/projects/tkpacman](https://archlinux.org/packages/?>pcurses</a></dd></dl>
<ul><li><b>tkPacman</b> — Tk pacman wrapper written in Tcl.</li></ul>
<dl><dd><a rel=) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)AUR