## 编译 U-Boot

```bash
# 建立并进入工作目录
TOP=$HOME/arm-linux
mkdir -p $TOP
cd $TOP
```

```bash
# 下载 U-Boot 源代码并解压：
# 从我在 Coding.net 上的一个仓库下载（国内地址）
# 但是没有文件大小显示，所以无法计算下载时间
curl https://coding.net/u/stamp711/p/arm-linux/git/raw/master/downloads/u-boot-2017.03.tar.gz | tar -xzf -
```

```bash
# 编译
cd u-boot-2017.03
make clean
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- vexpress_ca9x4_defconfig
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- all
```

```bash
# 在 QEMU 中测试
#【施工中】
```