## 编译 Busybox

【施工中】

---


最简单的 Linux 系统包括内核（Kernel）和根文件系统（RootFS），Linux内核启动后，会从根文件系统中寻找并执行 `init` 进程，这是系统的第一个进程，进程号是 `1`。所有的其他进程，都由 `init` 来启动。

Busybox 可以用来构建 RootFS。