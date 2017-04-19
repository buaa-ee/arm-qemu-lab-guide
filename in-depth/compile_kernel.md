## 编译内核

【已完成】

---


### 进入工作目录

```bash
# 进入工作目录
TOP=$HOME/arm-linux
cd $TOP
```


### 下载内核源码

```bash
# 下载内核源代码并解压(85M)：
curl https://coding.net/u/stamp711/p/arm-linux/git/raw/master/downloads/linux-4.10.5.tar.xz | tar -xJf -
```

这里依然是从我在 Coding.net 的仓库上下载。如果你想要其他版本的内核可以告诉我（毕竟从国外下载很慢）。


### 编译内核

```bash
# 进入内核源码目录
cd linux-4.10.5

# 使用 vexpress 的默认编译配置
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- vexpress_defconfig

# 可以在菜单中进一步修改配置（其实不用改）
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- menuconfig
```

```bash
# 进行编译
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- all
```


### 在 QEMU 中测试

```bash
# 在 QEMU 中测试
TOP=$HOME/arm-linux
DTB=$TOP/linux-4.10.5/arch/arm/boot/dts/vexpress-v2p-ca9.dtb
KERNEL=$TOP/linux-4.10.5/arch/arm/boot/zImage

qemu-system-arm -M vexpress-a9 -dtb $DTB -kernel $KERNEL -append "console=tty0" -serial stdio
```

上述命令将会模拟一个 `vexpress` 开发板，并且在上面启动编译好的 Linux 内核。如果你想要了解更多关于 QEMU 命令参数的信息，可以查看 [QEMU 启动选项说明](/appendix/qemu-opts.md)。

和之前一样，为了让命令具有可读性，我使用了变量：`DTB` 用来指代设备树文件，`KERNEL` 用来指代编译好的内核镜像文件。这些变量会在关闭终端后消失，需要重新设置。或者你可以不使用变量，但要输入一长串的 `qemu-system-arm...`命令。

当然，内核启动后发现没有根文件系统（`RootFS`），它无事可做，于是发生了 **内核失败（Kernel panic）**。

![测试结果](/assets/qemu_kernel_only.png)