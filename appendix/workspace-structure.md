## 工作目录安排

以下是目录树结构（在完成所有工作后使用 `tree -L 1` 命令生成）。

```
arm-linux
├── busybox-1.26.2
├── linux-4.10.5
├── rootfs
├── rootfs-by-apricity
├── rootfs.ext3
└── u-boot-2017.03
```


`arm-linux`：顶层工作目录
`busybox-1.26.2`：Busybox 源代码目录
`linux-4.10.5`：Linux 内核源代码目录
`rootfs`：我们制作的 RootFS 目录，同时也作为 NFS 所挂载的目录
`rootfs-by-apricity`：我对于 RootFS 的修改
`rootfs.ext3`：打包的 RootFS 镜像，可直接作为 vexpress 开发板的 SD 卡
`u-boot-2017.03`：U-Boot 源代码目录