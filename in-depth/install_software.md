## 安装所需的软件

在虚拟机桌面中，按 `Ctrl + Alt + T` 打开终端。

> **Info** 下文中，用 `$` 来表示命令提示符，`$` 之后是要输入的命令。**如果你喜欢 COPY/PASTE，不要将 `$` 包含在你的复制里！**
> **Info** `sudo` 表示以 ROOT 权限来执行后面的命令，你需要具有管理员权限的账户才能使用 `sudo`。使用 `sudo` 时，你需要输入密码；输入密码后，在一段时间内再次使用 `sudo` 将不需要输入密码。


* 为了获得更快的下载速度，我们更改 APT 的源为清华大学 TUNA 镜像源:

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


* 更新软件源列表：

    ```bash
    $ sudo apt-get update
    ```


* 安装交叉编译器：

    ```bash
    # -y 表示无需确认
    $ sudo apt-get install -y gcc-arm-linux-gnueabi g++-arm-linux-gnueabi
    ```


* 安装 QEMU：

    ```bash
    $ sudo apt-get install -y qemu
    ```
    > 安装QEMU时，`qemu-system` 和 `qemu-utils` 会被自动安装，所以不需要手动输入。


* 查看 QEMU 的版本信息：

    ```bash
    $ qemu-system-arm --version
    ```