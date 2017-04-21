## 安装软件

【状态：已完成】

---


```bash
# 为了获得更快的下载速度，我们让 APT 使用清华大学 TUNA 镜像源
# 先备份一下软件源列表免得出事情
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bakup

# 然后替换一下地址...
sudo sed -i "s|//.*archive.ubuntu.com|//mirror.tuna.tsinghua.edu.cn|" /etc/apt/sources.list
```

```bash
# 更新一下软件源列表
sudo apt-get update
```

```bash
# 安装一些要用到的东西
sudo apt-get -y install libncurses5-dev curl git
```

```bash
# 安装交叉编译器
# -y 表示无需确认
sudo apt-get install -y gcc-arm-linux-gnueabi g++-arm-linux-gnueabi
```

```bash
# 安装 QEMU
sudo apt-get install -y qemu-system
```