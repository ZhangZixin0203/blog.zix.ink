---
title: 低成本高效率使用Vercel&Github部署Hexo博客
top: 0
copyright: true
date: 2024-11-23 17:00:00
updated: 2024-11-24 9:00:00
permalink:
password:
comments:
tags: [Hexo, Nodejs, Website]
categories: 
    - [实践]
    - [系列,博客实践]
    - [教程]
keywords:
description:
---
在一年多的停止更新中，我曾经不只一次选择并更换托管商与博客软件。因为个人的技术原因以及在Windows上使用NPM的种种“水土不服”，所以最终转向了Wordpress+租用服务器的方式搭建博客。优点显著，方便、人性化、个性化。但因为其成本之高昂，让我一个学生党没有时间和精力去维护，于是个人博客得以搁置。（不是我懒）不过最近我安装了Ubuntu系统，就可以开发和娱乐分离，方便管理。

> 特别强调：本篇文章仅仅记录和提供最基础的思路，仅仅是在Ubuntu系统上实践，并没有深入展开。

<!--more-->
## 准备工作
前面提到，因为我在Windows系统上操作NPM和Git经常会遇到种种问题，于是乎我就把之前组的那一台洋垃圾的SATA固体装到了电脑上，将Linux系统挂载到了上面。
### 内容
- 16GB U盘
- Ubuntu[系统镜像](https://cn.ubuntu.com/download)
- 50GB的固态硬盘

具体安装Ubuntu系统我就不过多赘述了，可以去[这里](https://www.bilibili.com/video/BV1554y1n7zv/)查看。
## 环境搭建
### Git
由于我们需要Github与Vercel作为服务器进行搭建，所以[Git](https://git-scm.com/)肯定是必须的，你可以通过如下方式安装Git（Ubuntu系统终端下）：
```
sudo apt-get install git
```
执行完毕后运行`git -v`进行测试
### NPM & NODE
因为Hexo是基于Node的程序，所以[Node.js](https://nodejs.org/zh-cn)和它的包管理器[NPM](https://npm.nodejs.cn/)是必须的。
#### 方法一：使用包管理器安装
```
sudo apt update
sudo apt install nodejs
sudo apt install npm
node -v
```
> 特别强调：这种方法下载可能并非最新版。
#### 方法二：使用NVM下载
去[这里](https://nodejs.org/en/download/package-manager)**选择合适的版本**复制一下安装命令，比如说我在24年11月24日看到的是：
```
# installs nvm (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash

# download and install Node.js (you may need to restart the terminal)
nvm install 22

# verifies the right Node.js version is in the environment
node -v # should print `v22.11.0`

# verifies the right npm version is in the environment
npm -v # should print `10.9.0`
```
### 与Github建立连接
通常来讲，我们添加远程仓库，每一次操作远程仓库，都需要输入密码。所以说我们就需要用SSH方式（密钥）来与Github进行连接。   
这里我同样不过多赘述，当然以后我还是会出一部分关于SSHkey的内容。暂时可以看[这里](https://zhuanlan.zhihu.com/p/688103044)进行操作。
## 正式开始部署博客
### 本地
首先打开你的终端，**确保你在``~``中**，创建一个文件夹，进入，并全局安装Hexo，初始化Hexo再初始化Git。
```
mkdir blog ##文件夹名称随意

npm install -g hexo-cli ##全局安装Hexo

cd blog ##进入博客文件夹

hexo init ##初始化Hexo

git init ##初始化Git
```
> 特别强调：尽量不要把这些命令堆一块运行。
### 远程
登录到[Github](https://github.com)上，创建一个新仓库。命名随意。
> 特别强调：如果你要部署到Github pages上，请将仓库名改为YourID.github.io
> 不过这样可能需要在本地执行命令，不能直接提交到远程部署。（用Github Actions也行）

将你的本地仓库与远程[建立连接](https://geek-docs.com/git/git-questions/3_git_git_connect_existing_local_repository_to_existing_remote_repository.html)
> 特别强调：请使用SSH方式连接！如果无法使用再换成Https连接。并且建议用main作为主要分支。

当然，这一部分我后面单独出文章说明。连接成功后，先将所有内容提交：
```
git add . ##将目录下所有内容提交到暂存区
git commit -m "首次提交" ##提交
git push -u origin main ##如果前一步用main，这里也是main
```
### 部署到Vercel
登录到[Vercel](https://vercel.com/)，注册并登录以后，一般会直接提示你选择连接Github，然后选择仓库，就选择刚刚你创建的仓库。然后项目类型搜索Hexo。等待提示部署完成，此时，你可以绑定你自己的域名（可选，建议）。然后就可以访问了！
## 下一期
pid2：记录在Ubuntu下安装包时遇到的问题【完成】
### 同系列
pid3：低成本高效率使用Vercel&Github后期运维内容