## 编译 U-Boot

【状态：已完成】

---


### 建立并进入工作目录

```console
TOP=$HOME/arm-linux
mkdir -p $TOP
cd $TOP
```

注意：为了方便表述，这里使用了变量（变量在关闭终端后会消失，需要重新设置），你也可以不使用，直接把变量换成相应的文本即可。

上述命令的意义是：
* `TOP=$HOME/arm-linux`

    设定一个变量 `TOP` 用来指代顶层目录

* `mkdir -p $TOP`

    新建 `$TOP` 这个目录（`$TOP` 指的是变量 `TOP` 的内容）


### 下载 U-Boot 源码

这里下载的是 2017.03 的版本：

```console
# 下载 U-Boot 源码并解压(15M)
# 从 Coding.net 上的一个仓库下载（国内地址）
# 但是没有文件大小显示，所以无法看到剩余下载时间
curl https://coding.net/u/stamp711/p/arm-linux/git/raw/master/downloads/u-boot-2017.03.tar.gz | tar -xzf -
```

上面的命令使用了传输工具 `curl` 下载了一个 `tar.gz` 格式的压缩包，并把下载的内容通过管道直接传递给解压程序 `tar`。运行的结果：当前目录下出现解压后的文件夹 `u-boot-2017.03`。

<ftp://ftp.denx.de> 的下载速度非常慢，除非你有代理。如果你想要其他版本的 U-Boot 源码而又嫌下载速度太慢，可以告诉我。


### 编译 U-Boot

```console
# 进入源码目录
cd u-boot-2017.03
```

```console
# 为 vexpress 开发板生成配置文件
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- vexpress_ca9x4_defconfig
```
> vexpress 是一个 ARM 的开发板。可以参看 [这篇博客](https://learningfromyoublog.wordpress.com/2016/04/05/131/)。

```console
# 进行编译
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- all
```

编译可能需要两到三分钟。如果你遇到了故障，记得要先使用 `make clean` 清除残留文件，然后再进行编译尝试。


### 在 QEMU 中测试

```bash
# 在 QEMU 中测试
TOP=$HOME/arm-linux
UBOOT=$TOP/u-boot-2017.03/u-boot

qemu-system-arm -M vexpress-a9 -kernel $UBOOT -serial stdio
```

上述命令将会模拟一个 `vexpress` 开发板，并且将当前的终端连接到这个开发板的串口。由于我们没有指定内存大小，内存将默认为 128 MB。如果你想要了解更多关于 QEMU 命令参数的信息，可以查看 [QEMU 启动选项说明](/appendix/qemu-opts.md)。

为了让命令具有可读性，这里使用了变量 `UBOOT`，它指向的是编译好的二进制文件 `$TOP/u-boot-2017.03/u-boot`（注意 `$TOP` 指的是 `TOP` 变量的内容，也就是我们的顶层文件夹）。

这些变量会在关闭终端后消失，需要重新设置。或者你可以不使用变量，但要输入一长串的 `qemu-system-arm...`命令。

开机后，U-Boot 会尝试以各种方式启动。不过，由于我们还没有任何可以启动的操作系统，所以会提示 `ERROR`。就酱紫。

![测试结果](/assets/qemu-uboot-only.png)