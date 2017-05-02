# 运行 C 语言程序

```bash
# 进入工作目录
TOP=$HOME/arm-linux
cd $TOP
```

```bash
# 将 C 运行库拷贝到 RootFS 里面
mkdir -p $TOP/rootfs/lib
cp -a /usr/arm-linux-gnueabi/lib/* $TOP/rootfs/lib/
```

```bash
# 到 rootfs 目录下面
cd $TOP/rootfs/lib

# 用你喜欢的编辑器写一个 C 语言程序

# （你可能需要 sudo apt-get install gedit）
gedit hello.c
# 或者...
nano hello.c
# 再或者...
vim hello.c
```

```bash
# 写完之后，用交叉编译工具去编译它
# 不指定输出文件名的话，默认生成 a.out
arm-linux-gnueabi-gcc hello.c
```

```bash
# 启动
# 依然是使用 NFS 来作为 RootFS
# 注：不要修改 10.0.2.2 这个地址（参见 QEMU 使用手册）

TOP=$HOME/arm-linux
DTB=$TOP/linux-4.10.5/arch/arm/boot/dts/vexpress-v2p-ca9.dtb
KERNEL=$TOP/linux-4.10.5/arch/arm/boot/zImage

qemu-system-arm -M vexpress-a9 -dtb $DTB -kernel $KERNEL -append "root=/dev/nfs console=tty0 nfsroot=10.0.2.2:/$TOP/rootfs rw ip=dhcp"
```

```bash
# 在 QEMU 虚拟出的机器开机后，在它的命令行里输入
./a.out
```
