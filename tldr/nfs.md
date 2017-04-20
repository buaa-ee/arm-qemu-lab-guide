## 使用 NFS

【施工中】

---


```bash
# 安装 NFS 服务器
sudo apt-get install nfs-kernel-server
```

```bash
# 编辑 /etc/exports
sudo vim /etc/exports
```

```vim
# 加入像下面这一样的一行
# 注意修改 rootfs 文件夹的路径，对应在 $TOP/rootfs（TOP 是我们的顶层文件夹）
# 我的是 /home/apricity/arm-linux/rootfs
/home/apricity/arm-linux/rootfs 127.0.0.1(rw,sync,no_subtree_check,no_root_squash,insecure)
```

```bash
# 启动
TOP=$HOME/arm-linux
DTB=$TOP/linux-4.10.5/arch/arm/boot/dts/vexpress-v2p-ca9.dtb
KERNEL=$TOP/linux-4.10.5/arch/arm/boot/zImage

qemu-system-arm -M vexpress-a9 -dtb $DTB -kernel $KERNEL -append "root=/dev/nfs console=tty0 nfsroot=10.0.2.2:/$TOP/rootfs rw ip=dhcp"
```