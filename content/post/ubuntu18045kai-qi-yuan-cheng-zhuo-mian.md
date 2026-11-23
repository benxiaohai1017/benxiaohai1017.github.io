---
title: "Ubuntu 18.04.5 开启远程桌面"
date: 2021-02-15T09:26:07+08:00
lastmod: 2026-10-20T16:06:37+08:00
categories: []
tags: []
draft: false
---

使用 VNC 协议（显示 Ubuntu 原始 gnome 桌面）。

## 1. 远程 server 的设置

打开 **设置 → 共享**，将「允许他人远程连接控制该电脑」开启。

如果不能开启或者没有这个选项，则可能需要安装 vino——我就是安装了 vino 才有了这个选项：

```bash
sudo apt install vino
```



安装 vncserver 的依赖包：

```bash
sudo apt-get install xrdp xbase-clients
```

安装 dconf-editor：

```bash
sudo apt-get install dconf-editor
```

取消权限限制：打开 dconf-editor，依次展开 `org → gnome → desktop → remote-access`，然后取消 `require-encryption` 的勾选。


## 2. 本地机器设置

打开系统自带的远程访问工具：Windows 的远程连接（mstsc）或者 Ubuntu 的 Remmina，或者下载 VNC Viewer。

选择 VNC-any 或者 console，输入 IP 和密码即可。

## 注意事项

切记不要在 server 中安装太多版本的 vnc server。使用 `dpkg -l | grep -i "vnc"` 搜索 server 中安装的 vnc server，只保留最简配置即可：

- `vino` 是保证其他机器远程到本机的
- `libvncclient1:amd64` 和 `remmina-plugin-vnc` 是使用 Remmina 远程至其他机器的
- 其他 vnc 相关的包都可以卸载

使用 vnc 协议进行远程的时候，是需要依赖 `xrdp` 和 `xorgxrdp` 这两个包的。
