---
title: 给使用Docker的容器安装QEMU以运行Windows
categories: 白嫖系列
tags:
  - Docker
  - Windows
  - QEMU
  - Proot
  - 麦块联机
  - 免费
  - 挂机宝
date: 2024-12-29 00:00:00
updated: 2024-12-29 15:00:00
cover: //cdn.qwqo.cn/file/xjh/0a9718d886f452a10997aa4efd836eeb.png
---

## 给使用Docker的容器安装QEMU以运行Windows

最近看到某面板服大力投流 并且免费的配置高达8核心24G
那是咸是屎总该尝一尝
然后整好最近还想扩充一下免费共享挂机宝
就准备给这玩意装个Windows
需要下载 [alpian](https://api.kxzjoker.cn/API/123pan.php?url=https%3A%2F%2Fwww.123865.com%2Fs%2FfZA0Vv-687ud.html&type=down) [proot](https://api.kxzjoker.cn/API/123pan.php?url=https%3A%2F%2Fwww.123865.com%2Fs%2FfZA0Vv-y87ud.html&type=down) 以及 系统镜像 三个文件

### 先进入Proot

``` bash
./dist/proot -S . /bin/ash
```

### 安装QEMU

``` bash
apk add qemu qemu-system-x86_64 qemu-img
```

### 查看QEMU版本

``` bash
qemu-system-x86_64 --version
```

### 运行虚拟机

``` bash
qemu-system-x86_64 -m 内存G -smp 核心数 -drive file=/镜像文件.qcow2,format=qcow2 -device e1000,netdev=net0 -netdev user,id=net0,hostfwd=tcp::外部端口-:3389,hostfwd=udp::外部端口-:3389 -vga std -usb -device usb-tablet -boot order=c -vnc : VNC端口 端口-5900
```
例子
``` bash
qemu-system-x86_64 -m 16G -smp 8 -drive file=/2008r2.qcow2,format=qcow2 -device e1000,netdev=net0 -netdev user,id=net0,hostfwd=tcp::25567-:3389,hostfwd=udp::25567-:3389 -vga std -usb -device usb-tablet -boot order=c -vnc :19666
```
### 最终效果

这东西始终还是屎
这个硬盘速度 现在是100多台服务器跑在一个2T的单盘
也是为难他了
![](//cdn.qwqo.cn/file/xjh/0a9718d886f452a10997aa4efd836eeb.png "硬盘IO")
![](//cdn.qwqo.cn/file/xjh/1dc96a4061dc9a47fb694d818d75e6d4.png "速度")


### 系统镜像

这个是qcow2硬盘文件
你可以前往轻舟云，rstack ,魔方云 这些地方下载 魔方云密码不太清楚但是硬盘占用最小
