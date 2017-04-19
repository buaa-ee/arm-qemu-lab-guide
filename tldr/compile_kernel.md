## 编译内核

【状态：已完成】

---


```bash
# 进入工作目录
TOP=$HOME/arm-linux
cd $TOP
```

```bash
# 下载内核源代码并解压(85M)：
curl https://coding.net/u/stamp711/p/arm-linux/git/raw/master/downloads/linux-4.10.5.tar.xz | tar -xJf -
```

```bash
# 进入内核源码目录
cd linux-4.10.5

# 使用 vexpress 的默认编译配置
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- vexpress_defconfig

# 可以在菜单中进一步修改配置（不用改）
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- menuconfig
```

```bash
# 进行编译
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- all
```

```bash
# 在 QEMU 中测试
TOP=$HOME/arm-linux
DTB=$TOP/linux-4.10.5/arch/arm/boot/dts/vexpress-v2p-ca9.dtb
KERNEL=$TOP/linux-4.10.5/arch/arm/boot/zImage

qemu-system-arm -M vexpress-a9 -dtb $DTB -kernel $KERNEL -append "console=tty0" -serial stdio
```

![测试结果](/assets/qemu_kernel_only.png)