## 编译 U-Boot

### U-Boot的编译

* 转到主文件夹，建立并进入工作目录：
    ```console
    # 可以用 '&&' 来在一行中输入多个命令
    $ cd $HOME && mkdir apricity && cd apricity
    ```


* 下载 U-Boot 源代码并解压，这里下载的是 2017.03 的版本：
    ```console
    # 从我在 Coding.net 上的一个仓库下载（国内地址）
    # 但是没有文件大小显示，所以无法计算下载时间
    curl https://coding.net/u/stamp711/p/arm-linux/git/raw/master/downloads/u-boot-2017.03.tar.gz | tar -xzf -
    ```
    ```console
    # 解压并进入目录
    $ tar -xzf u-boot-2017.03.tar.gz
    $ cd u-boot-2017.03
    ```
    > 不要去 <ftp://ftp.denx.de> 下载，除非你有代理。
    > 这个文件的大小是 14.92 M，在国内直接下载可能比较慢（大概要三四分钟吧）。我没找到靠谱的国内镜像源，所以也没办法了 T_T



* Make!
    ```console
    # 设置环境变量
    $ export ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
    ```
    > **这样设置的环境变量仅对当前终端有效。**如果你重新打开了终端并且想要使用 `make` 进行交叉编译，你需要再次设置。
    > 我个人不喜欢像实验指导书上那样修改 Makefile 文件。

    ```console
    # 生成配置文件
    $ make vexpress_ca9x4_defconfig
    ```
    > vexpress 是一个 ARM 的开发板。可以参看 [这篇博客](https://learningfromyoublog.wordpress.com/2016/04/05/131/)。

    ```console
    # 进行编译
    $ make
    ```
    > 如果你遇到了故障，记得要先使用 `make clean` 清除残留文件，然后再进行编译尝试。如果你退出了终端会话，那么还需要重新设置环境变量。
    > 使用 `-j` 选项可以进行多线程编译，线程个数会被自动设置为 CPU 的线程数。相应的命令为 `make -j`。但是有些情况下，多线程编译会出现一些稀奇古怪的问题，所以这里不使用。


### U-Boot 的运行

【施工中】