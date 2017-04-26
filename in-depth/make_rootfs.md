# 制作 RootFS

现在，我们使用编译好的 Busybox 来构建一个 RootFS，让内核启动后有事可做。

## 进入工作目录

```bash
TOP=$HOME/arm-linux
cd $TOP
```

## 建立目录结构

```bash
mkdir rootfs
cd rootfs
mkdir proc sys dev etc tmp
```

## 把 Busybox 复制进来

```bash
cp -a $TOP/busybox-1.26.2/_install/* .
cp -a $TOP/busybox-1.26.2/examples/bootfloppy/etc/* etc
```

## 进行一下必要的修改

主要是 `etc/fstab` 和 `etc/init.d/rcS` 两个文件。

下面的命令将会下载我的版本，并添加到 rootfs 文件夹。
这份文件仅供参考，你至少应该阅读一下它的内容。

> **注意：**类似于“可读”、“可写”等，“可执行”是 Linux 下文件属性的一种。如果你决定自己制作上述文件，请确保 `etc/init.d/rcS` 文件具有“可执行”的属性。可以通过使用 `chmod +x FILENAME` 来给文件加上（`+`）可执行（`x`）的属性。

```bash
cd $TOP
curl https://coding.net/u/stamp711/p/arm-linux/git/raw/master/downloads/rootfs-by-apricity.tar.gz | tar -xzf -
cp -a rootfs-by-apricity/* rootfs
```

## 制作镜像文件

我们不妨把要制作的镜像文件放在 `$TOP` 目录里，命名为 `rootfs.ext3`。

```bash
# 转到顶层文件夹
cd $TOP

# 生成一个大小为 32M 的、内容全为 0 的文件 rootfs.ext3
dd if=/dev/zero of=rootfs.ext3 bs=1M count=32

# 把这个文件上建立一个 Ext3 文件系统
mkfs.ext3 rootfs.ext3

# 将 rootfs.ext3 挂载到 tmpfs 文件夹下
# 你可以将这想象成类似“虚拟光驱”
mkdir -p tmpfs
sudo mount -o loop rootfs.ext3 tmpfs

# 把 rootfs 文件夹下的东西都拷进去
# 注意：向 tmpfs 文件夹下写入内容，就相当于写入了 rootfs.ext3
sudo cp -r rootfs/* tmpfs/

# 卸载挂载点，删除临时文件夹 'tmpfs'
sudo umount tmpfs
rmdir tmpfs
```

## 在 QEMU 中测试

```bash
TOP=$HOME/arm-linux
DTB=$TOP/linux-4.10.5/arch/arm/boot/dts/vexpress-v2p-ca9.dtb
KERNEL=$TOP/linux-4.10.5/arch/arm/boot/zImage
SD=$TOP/rootfs.ext3

qemu-system-arm -M vexpress-a9 -dtb $DTB -kernel $KERNEL -drive if=sd,index=0,file=$SD,format=raw -append "root=/dev/mmcblk0 console=tty0"
```

可以看到，我们做的 RootFS 在启动后给了我们一个终端，你可以试一试在里面输入命令。

看起来我们已经能在这块开发板上搞一些事情了。不过现在所有的用户态应用程序（即除了内核、驱动等）都是来自于我们刚刚编译的 Busybox（比如下图中在终端里运行的 `ls`）。在最后一章里，我们将会在这块开发板上运行自己写的 C 语言程序。

![测试结果](/assets/sd-rootfs.png)
![ls所指向的位置](/assets/sd-rootfs-ls.png)