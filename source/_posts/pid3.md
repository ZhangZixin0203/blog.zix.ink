---
title: 低成本高效率使用Vercel&Github后期运维内容
top: 0
copyright: true
date: 2024-11-25 8:00:00
updated: 2024-11-25 8:00:00
permalink:
password:
comments:
tags: [Hexo, Nodejs, Website, VSCode]
categories:
  - [实践]
  - [博客系列]
  - [教程]
keywords:
description:
---
在[上一期内容](/post/pid1)中，我成功在Vercel部署了博客。目前来看访问速度并不是很可以，这是因为Vercel服务器在海外，切换成海内服务器即可。但是我们要追求 **“低成本”**，租服务器是不可能的。于是在本章我将介绍一下**后期博客的维护、NexT主题的配置文件和我选用的Hexo插件**。<!--more-->
## Markdown编写
我们知道Hexo是将Markdown文档转换成静态HTML文件的博客生成程序，于是书写Markdown就成为了不可缺少的部分。编辑器这一方面我推荐[VSCode](https://code.visualstudio.com/)，支持多系统、效率高、UI舒服、有汉化、大厂出品、轻量化等等都是它的优点。

安装这一方面我就不过多赘述，在Linux和Windows下都可以方便、流畅的安装。下载安装完毕后，你大概会看到一个英文的界面，所以说请
### 切换成中文
我们单击一下最左边四个方格的`扩展`选项
> 特别注意：如果说你没有截图的第三个、第五个，而且是首次安装，属于正常现象。

![pid3-1](https://pic.imgdb.cn/item/6743339588c538a9b5bb66fc.png)

点击进入后，在上方搜索框搜索`简体中文`，选择最上面创作者为Microsoft的扩展。点击旁边的`install`。此时右下角应该会提示你进行选择并重启，按照要求重启程序即可。重启完毕后，没有问题应该就是中文了。

![pid3-2](https://pic.imgdb.cn/item/6743339688c538a9b5bb66fd.png)

### Markdown预览
Markdown作为一门标记语言，有预览肯定是更加方便的，于是我们可以增加一个Markdown预览插件。同样，打开`扩展`页面，搜索`Markdown All in One`由Yu Zhang所编写的。
安装成功后看到类似浏览器选项卡的最右边，随意选择一个`.md`文件，你会看到一个这样的图标：

![pid3-3](https://pic.imgdb.cn/item/6743339788c538a9b5bb66fe.png)

我们选择一个从右往左第三个，即是有一个放大镜的按钮，此时就打开了Markdown预览。当然，侧边选项卡也不仅仅可以作为预览选项卡，也可以多开文件，同时编辑等等。

![pid3-4](https://pic.imgdb.cn/item/6743339788c538a9b5bb66ff.png)

## Hexo文章
### 添加文章
#### 通过Bash
Hexo添加新文章通常在Bash中用
```
hexo n type "name"
```
来创建，比如说我要创建一个名为`低成本高效率使用Vercel&Github后期运维内容`的`文章`，需要输入
```
hexo n post "低成本高效率使用Vercel&Github后期运维内容"
```
然后如果Hexo弹出了创建成功之类的文本，即是创建成功。
#### 直接添加
直接在`./source/_posts/`中新建Markdown文件。**不建议**。
### 编辑
在VSCode中选择左侧最上面内容，打开`资源管理器`，将你博客文件夹添加进入，在**确保安全的情况下选择信任父文件夹**。再在`资源管理器`中找到`/source/_posts/name.md`，双击进入，即可编辑。
## 文章信息
如果你是[通过Bash](#通过Bsah)新建的文章，那么在文章最上方上方形如这样的内容
```
---
title: 
top: 0
copyright: true
date: 2024-11-24 18:22:45
updated: 2024-11-24 18:22:45
permalink:
password:
comments:
tags:
categories:
keywords:
description:
---
```
这些内容是跟目录下`/scaffolds`里面的Markdown内容有关。建议使用NexT主题将上者的`post.md`和`draft.md`改成这样。
- `title`文章标题，必填
- `top`文章首页排序，必填
- `copyright`版权，bool，必填
- `date`以及`updated` 创建时间和更新时间，必填
- `tags`标签，建议填写
- `categories`分类，建议填写
- `keywords`SEO关键词，建议填写
- `description`SEO描述，建议填写

剩余的便是需要从NexT主题里的扩展项，需要进入主题配置文件进行开启的，后面说到了再详细讲。这些内容有关于你的网站展示在用户前的相貌以及竞价排名，所以请务必认真填写。当然，如果你和我一样不在意SEO,基本上是给自己看，最后两者可以不填，因为它们不会直接在网站上显示出来。
### tags与categories的填写
转载自[hexo博客中tags与categories用法](https://zhuanlan.zhihu.com/p/348131730)
```
# 多标签写法，这2种都是一样的效果，用哪个都可以，建议使用列表[]式，直观清晰。
tags:
  - 123
  - 456
tags: [123, 456]

# 这是默认的写法，给文章添加一个分类。
categories: 123
# 这会将文章分类123/456子分类目录下。
categories: [123, 456]
这会将文章分类到123/456子分类目录下。
categories:
   - 123
   - 456
多分类写法，文章被分类到123、456以及123的自分类789这3个分类下面，官方指定写法。
categories:
   - [123]
   - [456]
   - [123, 789]
```
`更新中`