## 编译 Busybox

【施工中】

---


最简单的 Linux 系统包括内核（Kernel）和根文件系统（RootFS），Linux内核启动后，会从根文件系统中寻找并执行 `init` 进程，这是系统的第一个进程，进程号是 `1`。所有的其他进程，都由 `init` 来启动。

Linux 发行版之间根本的区别就在于它们的 RootFS。Busybox 是一个工具集，可以用来构建 RootFS。


### 进入工作目录

```bash
# 进入工作目录
TOP=$HOME/arm-linux
cd $TOP
```


### 下载 Busybox 源代码并解压

```bash
# 下载 Busybox 源代码并解压：
curl https://coding.net/u/stamp711/p/arm-linux/git/raw/master/downloads/busybox-1.26.2.tar.bz2 | tar -xjf -
```

这里依然是从 Coding.net 的仓库上下载。如果你想要其他版本的 Busybox 源码，而又嫌从国外下载速度太慢，可以告诉我。


### 编译 Busybox

```
# 进入 Busybox 源码目录
cd busybox-1.26.2

# 去菜单中修改配置
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- menuconfig
# Busybox Settings —> Build Options —> [*] Build BusyBox as a static binary (no shared libs)
```

![](/assets/busybox_menuconfig_1.png)  
![](/assets/busybox_menuconfig_2.png)

这是为了让 Busybox 被编译成静态的二进制文件，即无须外部“动态链接库”即可运行。


```bash
# 进行编译
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- install
```

请喝茶