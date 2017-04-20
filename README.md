# QEMU 模拟 Cortex-A9 运行 U-boot 和 Linux

Made with ❤️ by APRICITY

【现在可以点击左侧导航来进入相应章节】


## 施工说明 🚧

本 GitBook 尚在施工中。如果你发现网页连接不上了，那么很有可能是因为 **更新正在被推送到树莓派上**。一般来说这个时间不会超过 1 分钟。

完成的页面标题下方标有有【状态：已完成】，你可以直接按照页面尝试。在所有页面都完成后，这些标志将被删去。未完成的页面可能是没有写完，也可能是没有经过测试。


## 注意 🔮

** 你无需（也不建议）随意使用 `root` 权限，更不要直接以 `root` 用户身份进行操作。**这样很危险。

本文中使用的 U-Boot、Linux 内核、Busybox 等均为较新的版本。如果使用的版本和本文一致，**你无需（也不建议）修改 Makefile 或者其他的任何源代码。**

为了方便表述，本文在命令行中使用了变量，**变量在关闭终端后会消失，需要重新设置。**你也可以不使用，直接把变量换成相应的文本即可。

本文中的步骤都是经过仔细考虑了的，虽然其中很多做法的原因都没有写出来（因为懒 T_T）。如果你想要进一步了解，可以找你身边比较熟悉 Linux 的人，或者联系我。


## 在开始之前... 🤔

本文对于工作目录（也就是文件夹）的安排见这里：[工作目录安排](appendix/workspace-structure.md)

如果你对 Linux 的命令行还不是很熟悉，可以看这里：[熟悉命令行](appendix/intro-commandline.md)

为了提高下载速度，我已将所需的文件上传到 Coding.net（国内）的一个仓库中。本文中所有的下载地址均来源于 Coding.net。

本文使用的发行版是 XUbuntu 16.04.2 LTS，虚拟化软件是 VirtualBox。如果你使用的是原版 Ubuntu，也没有关系，它们只是桌面环境长得不一样而已。

