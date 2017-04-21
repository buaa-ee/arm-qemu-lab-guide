## 运行 C 语言程序

【施工中】

---


```bash
# 进入工作目录
TOP=$HOME/arm-linux
cd $TOP
```

```bash
# 将 C 运行库拷贝到 RootFS 里面
mkdir -p $TOP/rootfs/lib
cp -a /usr/arm-linux-gnueabi/lib/* $TOP/rootfs/lib/
```

```bash
# 到 rootfs 目录下面
cd $TOP/rootfs/lib

# 用你喜欢的编辑器写一个 C 语言程序

# （你可能需要 sudo apt-get install gedit）
gedit hello.c
# 或者...
nano hello.c
# 再或者...
vim hello.c
```

```
# 写完之后，用交叉编译工具去编译它
arm-linux-gnueabi-gcc hello.c
```