## 编译 Busybox

```bash
# 进入工作目录
TOP=$HOME/arm-linux
cd $TOP
```

```bash
# 下载 Busybox 源代码并解压：
curl https://busybox.net/downloads/busybox-1.26.2.tar.bz2 | tar -xjf -
```

```bash
# 配置编译
cd busybox-1.26.2
export ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-

# 去菜单中修改
make menuconfig
# Busybox Settings —> Build Options —> [*] Build BusyBox as a static binary (no shared libs)
```

![](/assets/busybox_menuconfig_1.png)  
![](/assets/busybox_menuconfig_2.png)

```bash
# 进行编译
make install
```



