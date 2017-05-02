# 使用 NFS

NFS，即网络文件系统(Network File System)，是由Sun公司1984年发布的分布式文件系统协议。

NFS 允许客户端上的用户像访问本地文件一样地访问网络上的文件。在客户端的机器看起来，远程主机的目录就好像是自己的一个磁盘分区一样！

现在，我们要以 NFS 作为 QEMU 中虚拟开发板的根文件系统（RootFS）。

## 安装 NFS 服务器

```bash
sudo apt-get install nfs-kernel-server
```

## 配置 NFS 共享的目录

完成 [制作 RootFS](/in-depth/make_rootfs.md) 之后，`$TOP/rootfs` 文件夹里应该有相应的根文件系统结构。
我们将把这个文件夹发布为 NFS 共享。

`/etc/exports` 是 NFS 的主要配置文件，你需要使用管理员权限去编辑它。

```bash
# 用你喜欢的编辑器编辑 /etc/export

# 你可能需要 sudo apt-get install gedit
sudo gedit /etc/exports
# 或者...
sudo nano /etc/exports
# 再或者...
sudo vim /etc/exports
```

在 `/etc/exports` 文件里，每一行代表了一个共享，格式为：

```plain
[分享目录]    [允许访问的主机(权限)]
```

我们要共享上一节里存放 RootFS 的文件夹，即 `$TOP/rootfs`。
所以，我们在 `/etc/exports` 里加入像下面这样的一行：

```vim
/home/apricity/arm-linux/rootfs 127.0.0.1(rw,sync,no_subtree_check,no_root_squash,insecure)
```

> 注意修改文件夹的路径，对应在 `$TOP/rootfs`，本文是`/home/apricity/arm-linux/rootfs`。
>
> 你可以到 [鸟哥的 Linux 私房菜][vbird] 查看更多有关该文件语法的信息。

[vbird]: http://cn.linux.vbird.org/linux_server/0330nfs.php#nfsserver_exports


保存文件之后，重启 NFS 服务：
```bash
sudo service nfs-kernel-server restart
```

## 启动 QEMU

这一次我们使用 NFS 来作为 RootFS。

在内核启动参数（即 `-append` 后面的内容）中：

* 使用 `root=/dev/nfs` 来指定内核从 NFS 启动，
* 使用 `nfsroot=...` 来告诉内核 NFS 共享的地址和读／写权限，
* 使用 `ip=dhcp` 来告诉内核通过 QEMU 提供的 DHCP 服务自动获取网络地址。

```bash
TOP=$HOME/arm-linux
DTB=$TOP/linux-4.10.5/arch/arm/boot/dts/vexpress-v2p-ca9.dtb
KERNEL=$TOP/linux-4.10.5/arch/arm/boot/zImage

qemu-system-arm -M vexpress-a9 -dtb $DTB -kernel $KERNEL -append "root=/dev/nfs console=tty0 nfsroot=10.0.2.2:/$TOP/rootfs rw ip=dhcp"
```

注：`10.0.2.2` 这个地址是 QEMU 钦定的访问主机（你的 Ubuntu 虚拟机）的地址。
