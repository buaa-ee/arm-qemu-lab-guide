## 在你的电脑上运行 Linux

【状态：已完成】

---

### 发行版的选择

为了和原实验指导书保持一致，本文使用的 Linux 发行版是 [XUbuntu](https://xubuntu.org)。

Ubuntu 官方考虑到使用者的不同需求，提供各种不同的发行版。这几种发行版本的差别在于桌面环境和预设安装的软件不同，但采用的套件库是一样的。这些发行版可以在 [Ubuntu Flavours](https://www.ubuntu.com/download/ubuntu-flavours) 下载。

XUbuntu 使用的桌面环境是 Xfce 而不是 Unity，因此占用的资源更少一些。如果你使用的是原版 Ubuntu，也没有关系。它们只是桌面环境长得不一样而已。
![XUbuntu](/assets/xubuntu.png)

如果下载速度太慢，可以去 [清华大学的 ISO 镜像站][TUNA-UbuntuISO] 下载。如果你想要从清华大学下载 `XUbuntu 16.04.2 LTS`，可以直接点击：[下载地址][XUbuntuDownload]。

[TUNA-UbuntuISO]:   https://mirrors.tuna.tsinghua.edu.cn/ubuntu-cdimage/
[XUbuntuDownload]:  https://mirrors.tuna.tsinghua.edu.cn/ubuntu-cdimage/xubuntu/releases/16.04.2/release/xubuntu-16.04.2-desktop-i386.iso


### 准备虚拟机

本文使用 [VirtualBox](https://virtualbox.org)，这里只对虚拟机的安装作一些简要的说明。

你应当进行的步骤有：

* 新建一个虚拟机，为其分配合理的 CPU、内存、磁盘。
    * 虚拟机类型选择 **64-bit Ubuntu**。
    * 建议启用动态分配磁盘文件大小的功能，这样可以节省宿主机的空间。
    * 如果在虚拟机中进行操作时感受到 **非常明显** 的卡顿，请尝试关掉虚拟机配置中的图形加速。


* 将安装光盘镜像（ISO 文件）加载到虚拟机的光驱中。


* 开启虚拟机，完成系统的安装。
    * 确保你在安装过程中设置了合适的用户名和密码。
    * **确保你创建的账户具有管理员权限**，否则后面会无法使用 `sudo` 命令。


* 安装虚拟机附加程序
    * 这种程序通常由虚拟机软件提供，用于虚拟机和宿主机的融合，安装以后才能正常使用一些功能（如**自动调节分辨率、自动挂载共享文件夹、与宿主机之间进行剪贴板共享**等）。
    * Ubuntu 的软件仓库提供了虚拟机附加程序，可以直接安装，详见章节 [安装所需的软件](/in-depth/install_software.md)。
    * 你应当在虚拟机软件的菜单中寻找“安装附加程序”的命令并点击。对于 VirtualBox，它看起来大概在这里：![菜单命令](/assets/menu-addons.png)
    * 通常情况下，附加程序作为一张虚拟光盘被插入虚拟机中，你可能需要手动进行安装。在光盘的根目录下打开终端，输入 `./autorun.sh` 并回车。输入你账户的密码来继续安装。
    ![在这里打开终端](/assets/install-addons-1.png)
    * 看到安装完成的提示后，按下回车键关闭安装程序，并重启虚拟机。
    ![安装完成](/assets/install-addons-2.png)