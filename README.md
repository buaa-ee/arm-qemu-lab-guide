# QEMU 模拟 Cortex-A9 运行 U-boot 和 Linux

Made with ❤️ by APRICITY

【请先阅读下面的说明】


## 施工说明 🚧

本 GitBook 尚在施工中。如果你发现网页连接不上了，那么很有可能是因为更新正在被推送到树莓派上。一般来说这个时间不会超过 1 分钟。

未完成的页面可能是没有写完，也可能是没有经过测试。


## 注意 🔮

你无需（也不建议）随意使用 `root` 权限，更不要直接以 `root` 用户身份进行操作。这样很危险。

本文中使用的 U-Boot、Linux 内核、Busybox 等均为较新的版本，你无需（也不建议）修改 Makefile 或者其他的任何源代码。

为了方便表述，本文在命令行中使用了变量，变量在关闭终端后会消失，需要重新设置。你也可以不使用，直接把变量换成对应的文本即可。

本文中的步骤都是经过了仔细考虑的，所以和老师给的实验指导书会有所不同。其中很多做法的原因都没有写出来（因为懒 T_T）。如果你想要进一步了解或者需要帮助，可以找你身边比较熟悉 Linux 的人，也可以联系我。


## 如果你看了老师发的实验指导书... 📜

最好不要将其与本文的做法混用，新发的实验指导书依然有些问题……

比如，在编译 Linux 内核的时候会同时生成设备树文件 `vexpress-v2p-ca9.dtb`，也需要传递给 QEMU，否则启动后是黑屏。我不确定实验指导书中的“修改源代码”是不是用来解决这个问题的（不管是不是我都不建议……尤其是当你不知道所改的东西会带来的具体影响之时）。

诸如此类。总之，你需要自己去思考。


## 在开始之前... 🤔

本文对于工作目录（也就是文件夹）的安排见这里：[工作目录安排](appendix/workspace-structure.md)

如果你对 Linux 的命令行还不是很熟悉，可以看这里：[熟悉命令行](appendix/intro-commandline.md)

为了提高下载速度，所需的文件已被上传到 Coding.net（国内）的一个仓库中。本文中所有的下载地址均来源于 Coding.net。

本文使用的发行版是 XUbuntu 16.04.2 LTS，虚拟化软件是 VirtualBox。如果你使用的是原版 Ubuntu，也没有关系，它们只是桌面环境长得不一样而已。

