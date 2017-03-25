```bash
# 进入工作目录
TOP=$HOME/arm-linux
cd $TOP
```

```bash
# 下载内核源代码并解压：
curl https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.10.5.tar.xz | tar -xJf -
```

```bash
# 配置编译
cd linux-4.10.5
export ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-

# 使用 vexpress 的默认配置
make vexpress_defconfig

# 可以在菜单中进一步修改配置
make menuconfig
```

```bash
# 进行编译
make
```

```bash
# 在 QEMU 中测试
TOP=$HOME/arm-linux
DTB=$TOP/linux-4.10.5/arch/arm/boot/dts/vexpress-v2p-ca9.dtb
KERNEL=$TOP/linux-4.10.5/arch/arm/boot/zImage

qemu-system-arm \
  -M vexpress-a9 \
  -m 256M \
  -dtb $DTB \
  -kernel $KERNEL \
  -append "console=tty0" \
  -serial stdio
```

![测试结果](/assets/qemu_kernel_only.png)