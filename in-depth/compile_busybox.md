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


```bash
# 下载 Busybox 源代码并解压：
curl https://coding.net/u/stamp711/p/arm-linux/git/raw/master/downloads/busybox-1.26.2.tar.bz2 | tar -xjf -
```

