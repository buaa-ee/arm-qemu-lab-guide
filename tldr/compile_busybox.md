## 编译 Busybox

【状态：已完成】

---


```bash
# 进入工作目录
TOP=$HOME/arm-linux
cd $TOP
```

```bash
# 下载 Busybox 源代码并解压：
curl https://coding.net/u/stamp711/p/arm-linux/git/raw/master/downloads/busybox-1.26.2.tar.bz2 | tar -xjf -
```

```bash
# 进入源码目录
cd busybox-1.26.2

# 去菜单中修改配置
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- menuconfig
# Busybox Settings —> Build Options —> [*] Build BusyBox as a static binary (no shared libs)
```

![](/assets/busybox_menuconfig_1.png)  
![](/assets/busybox_menuconfig_2.png)

```bash
# 进行编译
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- install
```

