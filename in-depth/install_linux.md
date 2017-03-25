## 在你的电脑上运行 Linux

### 发行版的选择
为了和原实验指导书保持一致，本文使用的 Linux 发行版是 [XUbuntu](https://xubuntu.org)。

Ubuntu 官方考虑到使用者的不同需求，提供各种不同的发行版。这几种发行版本的差别在于桌面环境和预设安装的软件不同，但采用的套件库是一样的。这些发行版可以在 [Ubuntu Flavours](https://www.ubuntu.com/download/ubuntu-flavours) 下载。

XUbuntu 使用的桌面环境是 Xfce 而不是 Unity，因此占用的资源更少一些。如果你使用的是原版 UBuntu，也没有关系。它们只是桌面环境长得不一样而已。
![XUbuntu](/assets/xubuntu.png)

如果下载速度太慢，可以去 [清华大学的镜像站][TUNA-UbuntuISO] 下载。如果你想要下载 `XUbuntu 16.04.2 LTS`，可以直接点击：[下载地址][XUbuntuDownload]。
[TUNA-UbuntuISO]:   https://mirrors.tuna.tsinghua.edu.cn/ubuntu-cdimage/
[XUbuntuDownload]:  https://mirrors.tuna.tsinghua.edu.cn/ubuntu-cdimage/xubuntu/releases/16.04.2/release/xubuntu-16.04.2-desktop-i386.iso

### 准备虚拟机
本文使用 [VirtualBox](https://virtualbox.org)，这里只对虚拟机的安装作一些简要的说明。

你应当进行的步骤有：

1. 新建一个虚拟机，为其分配合理的 CPU、内存、磁盘
    - 虚拟机类型选择 **64-bit Ubuntu**。
    - 建议启用动态分配磁盘文件大小的功能，这样可以节省宿主机的空间。
    - 如果在虚拟机中进行操作时感受到 **非常明显** 的卡顿，请尝试关掉虚拟机配置中的图形加速。

2. 将安装光盘镜像（ISO 文件）加载到虚拟机的光驱中

3. 开启虚拟机，完成系统的安装
    - 确保你在安装过程中设置了合适的用户名和密码。
    - **确保你创建的账户具有管理员权限**，否则后面会无法使用 `sudo` 命令。


4. 安装虚拟机附加程序（Guest Additions）
    - 这种程序通常由虚拟机软件提供，安装以后才能正常使用一些功能（如自动调节分辨率等）。
    - 你应当在虚拟机软件的菜单中寻找“安装附加程序”的命令并点击。对于 VirtualBox，它看起来大概在这里：![菜单命令](/assets/menu-addons.png)
	- 通常情况下，附加程序作为一张虚拟光盘被插入虚拟机中，你可能需要手动进行安装。在光盘的根目录下打开终端，输入 `./autorun.sh` 并回车。输入你账户的密码来继续安装。
        ![在这里打开终端](_image/AddonsInstall-1.png)
	- 看到安装完成的提示后，按下回车键关闭安装程序，并重启虚拟机。
        ![安装完成](./_image/AddonsInstall-2.png)

### 安装所需的软件
在虚拟机桌面中，按 `Ctrl + Alt + T` 打开终端。
> 下文中，用 `$` 来表示命令提示符，`$` 之后是要输入的命令。**如果你喜欢 COPY/PASTE，不要将 `$` 包含在你的复制里！**
> `sudo` 表示以 ROOT 权限来执行后面的命令，你需要具有管理员权限的账户才能使用 `sudo`。使用 `sudo` 时，你需要输入密码；输入密码后，在一段时间内再次使用 `sudo` 将不需要输入密码。

- 为了获得更快的下载速度，我们更改 APT 的源为清华大学 TUNA 镜像源:
    ```bash
    # 先备份一个
    $ sudo cp /etc/apt/sources.list /etc/apt/sources.list.bakup
    ```
    ```bash
    # 替换一个...啊不对是两个
    $ sudo sed -i 's/cn.archive.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/' /etc/apt/sources.list
    $ sudo sed -i 's/archive.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/' /etc/apt/sources.list
    ```
    > `sed` 只是简单地作了字符串的替换操作。上面的命令并不能替换列表中所有的软件源地址，不过之后需要进行大量下载的源已经被替换了。如果你有 IPV6 网络环境的话，在 TUNA 下载软件包是不会花费校园网流量的。

- 更新软件源列表：
    ```bash
    $ sudo apt-get update
    ```

- 安装交叉编译器：
    ```bash
    # -y 表示无需确认
    $ sudo apt-get install -y gcc-arm-linux-gnueabi g++-arm-linux-gnueabi
    ```

- 安装 QEMU：
    ```bash
    $ sudo apt-get install -y qemu
    ```
    > 安装QEMU时，`qemu-system` 和 `qemu-utils` 会被自动安装，所以不需要手动输入。

- 查看 QEMU 的版本信息：
    ```bash
    $ qemu-system-arm --version
    ```