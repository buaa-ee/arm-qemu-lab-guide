## 制作 RootFS

【状态：已完成】

---


```bash
# 进入工作目录
TOP=$HOME/arm-linux
cd $TOP
```

```bash
# 建立目录结构
mkdir rootfs
cd rootfs
mkdir proc sys dev etc tmp
```

```bash
# 把 Busybox 复制进来
cp -a $TOP/busybox-1.26.2/_install/* .
cp -a $TOP/busybox-1.26.2/examples/bootfloppy/etc/* etc
```

```bash
# 进行一下必要的修改
# 我打包了一份 rootfs-by-apricity.tar.gz，仅供参考
cd $TOP
curl https://coding.net/u/stamp711/p/arm-linux/git/raw/master/downloads/rootfs-by-apricity.tar.gz | tar -xzf -
cp -a rootfs-by-apricity/* rootfs
```

```bash
# 制作镜像文件
cd $TOP
dd if=/dev/zero of=rootfs.ext3 bs=1M count=32
mkfs.ext3 rootfs.ext3

mkdir -p tmpfs
sudo mount -o loop rootfs.ext3 tmpfs
sudo cp -r rootfs/* tmpfs/
sudo umount tmpfs
rmdir tmpfs
```

```bash
# 在 QEMU 中测试
TOP=$HOME/arm-linux
DTB=$TOP/linux-4.10.5/arch/arm/boot/dts/vexpress-v2p-ca9.dtb
KERNEL=$TOP/linux-4.10.5/arch/arm/boot/zImage
SD=$TOP/rootfs.ext3

qemu-system-arm -M vexpress-a9 -dtb $DTB -kernel $KERNEL -drive if=sd,index=0,file=$SD,format=raw -append "root=/dev/mmcblk0 console=tty0"
```

![测试结果](/assets/sd-rootfs.png)