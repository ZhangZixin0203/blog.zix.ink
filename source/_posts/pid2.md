---
title: 记录在Ubuntu下安装包时遇到的问题
top: 0
copyright: true
date: 2024-11-24 12:00:00
updated: 2024-11-25 21:00:00
permalink:
password:
comments:
tags: [Ubuntu,Fcitx,Debug,Edge]
categories:
    - [教程]
    - [实践]
keywords:
description:
---
上篇文章曾经提到过我为了重启博客又装了一个Ubuntu系统，这同时也是我第一次装Linux系统。现在我大部分环境都部署在ubuntu系统上。所以说一些实用必备的软件还是需要装的。
<!--more-->
## 输入法
### 前因
输入法我本来想选用装系统时自带的输入法，一是UI符合Ubuntu的设计，二是懒得装其他的。但是实际上，那一款输入法十分有九分不好用，使用起来甚至没有Windows11自带的输入法好用（Windows我也用的默认输入法）。一些词明显缺失。再加上该输入法莫名其妙崩溃了好多次，于是决定换搜狗输入法。

> Q：为什么不用Fcitx
>
> A：这东西莫名奇妙缺字，比如说我本来想打“终端”正常来说只需要输入`zhongduan`，但它会莫名少个字母。比如说变成`zhngduan`，`a`自己单蹦了。所以就会打不对字。

### 搜狗输入法的安装
实际上非常简单，只需要登录[搜狗输入法](https://shurufa.sogou.com/)下载deb包，再在本地执行`dpkg -i`即可，但是会出现依赖关系 `xxx - 仍未被配置`的问题，我尝试了网络上大多数办法，其中最常见的是：
```
sudo apt-get -f install
```
进行修复依赖。事实上，虽然部分情况下有用，但是对搜狗这个包无效果，仍然呈现`xxx - 仍未被配置`。于是我继续进行排查，尝试了多遍后，最终找到了`sudo apt autoremove`于是我执行了：
```
sudo apt autoremove
sudo apt-get -f install
```
然后成功安装。据网络上与我遇到同样问题的同志所说：
> 但这并不是依赖问题，使用sudo apt-get -f install　无法解决。其实问题是因为这几个软件包没有被完全安装或卸载。——[Ayknims on CSDN](https://blog.csdn.net/s306205127/article/details/78546484)

这算是CSDN最有用的一次。

### 搜狗输入法闪屏问题【2024年11月25日补充】
这同样是我遇到的问题，解决方式就是修改为X11模式。
<br/>详细步骤：
```
# 使用Gedit打开
gedit /etc/gdm3/custom.conf 
# 如若这一步提示没有Gedit这个命令，请执行
sudo apt-get update
sudo apt-get install gedit
```
将`WaylandEnable=false`这一行内容取消注释即可。
## Github无法连接
因为我同样也是一位游戏玩家，在Windows系统时常用WattTokkit来加速Steam、Github、人机验证等。但是在Linux系统上我了解到一款名为[dev-sidecar](https://github.com/docmirror/dev-sidecar)的开源项目。目前在github上有着16k的stars。

这款开源项目提供了NPM、Github、Git.exe、Stack Overflow的加速，个人体验下来速度非常不错，不过就是一开始使用可能有些小问题。[Linux安装传送门](https://github.com/docmirror/dev-sidecar/blob/master/doc/linux.md)。

> 特别提醒：有依赖问题可以参考[输入法](#输入法)部分。

### Edge浏览器证书安装
安装文档里没有提到，我在这里顺一嘴：
#### Step 1. 打开设置
![pid2-1](https://pic.imgdb.cn/item/6742b02188c538a9b5bb420c.png)
#### Step 2. 搜索证书
![pid2-2](https://pic.imgdb.cn/item/6742b02288c538a9b5bb420e.png)
#### Step 3. 添加证书
![pid2-3](https://pic.imgdb.cn/item/6742b02288c538a9b5bb420f.png)
选择完毕后询问时，记得把三个□都√上！
> 特别提醒：如果看不见cart证书文件的话，主要有没有显示**隐藏文件**！

## 截图软件
实话说，Linux的截图软件真心好看，不过功能很少，操作个人不是很喜欢与习惯。正好QQNT架构（塞浏览器）也是支持Linux系统的，而且安装十分通常，加上沟通的需要，于是直接安装了QQ9，目前体验下来与Windows上的无异。而且安装包下载特别快，几乎是一瞬之间。

## 浏览器
Windows上我只用Edge，所以说我在Linux系统上也选择了Edge。与QQ的截图软件一样都是我个人的使用习惯，没有绝对的好坏。也主要是因为我大部分密码和收藏夹都在Edge上，使用Edge也可以提高效率。最主要的一点是它的插件[商店加载](https://microsoftedge.microsoft.com/addons?hl=zh-CN)速度最快。

因为在我所找到的[官方下载页面](https://www.microsoft.com/zh-cn/edge/download?)一开始没有找到Linux版本，私以为是没有，但实际上在另一个[页面](https://www.microsoft.com/zh-cn/edge/)上（[详细安装教程传送门](https://www.sysgeek.cn/ubuntu-install-microsoft-edge/)），为了防止我以后自己找不到，贴出来放这了。

## 参考文献
- [Ubuntu出现依赖关系问题 - 仍未被配置问题 - C(出)S(生)DN](https://blog.csdn.net/s306205127/article/details/78546484)
- [dev-sidecar/README.md](https://github.com/docmirror/dev-sidecar/blob/master/README.md)
- [如何在 Ubuntu 上安装 Microsoft Edge 浏览器](https://www.sysgeek.cn/ubuntu-install-microsoft-edge/)

## 下一期
pid3：低成本高效率使用Vercel&Github后期运维内容【完成】