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
  - [系列,博客实践]
  - [教程]
keywords:
description:
---
在[上一期内容](/post/pid1)中，我成功在Vercel部署了博客。目前来看，编写效率太低，如果用随便一个文本编辑器，没有代码高亮写起来很难受。同时本章我还将介绍**后期博客的维护、NexT主题的配置文件和我选用的Hexo插件**。<!--more-->
## Markdown编写
我们知道Hexo是将Markdown文档转换成静态HTML文件的博客生成程序，于是书写Markdown就成为了不可缺少的部分。编辑器这一方面我推荐[VSCode](https://code.visualstudio.com/)，支持多系统、效率高、UI舒服、有汉化、大厂出品、轻量化等等都是它的优点。

安装这一方面我就不过多赘述，得益于VSCode傻瓜式的安装，在Linux和Windows下都可以方便、流畅的安装。下载安装完毕后，你大概会看到一个英文的界面，对于英文不太好的同志，还是切换成中文更加方便。
### 切换成中文
我们单击一下最左边四个方格的`扩展`选项
> 特别注意：如果说你没有截图的第三个、第五个，而且是首次安装，属于正常现象。

![pid3-1](https://pic.imgdb.cn/item/6743339588c538a9b5bb66fc.png)

点击进入后，在上方搜索框搜索`简体中文`，选择最上面创作者为Microsoft的扩展。点击旁边的`install`。此时右下角应该会提示你进行选择并重启，按照要求重启程序即可。重启完毕后，没有问题应该就是中文了。

![pid3-2](https://pic.imgdb.cn/item/6743339688c538a9b5bb66fd.png)

### 为Markdown添加预览
我们可以增加一个Markdown预览插件，“所见即所得”让我们的编写更加方便。同样，打开`扩展`页面，搜索由Yu Zhang所编写的`Markdown All in One`。
安装成功后请先随意选择一个`.md`文件，找到看到类似浏览器选项卡一栏的最右边：

![pid3-3](https://pic.imgdb.cn/item/6743339788c538a9b5bb66fe.png)

我们选择从右往左数第三个按钮，Markdown预览。此时，应该可以在侧边栏里看到Markdown预览。当然，侧边选项卡也不仅仅可以作为预览选项卡，也可以多开文件，同时编辑等等。这部分内容不详细展开。

![pid3-4](https://pic.imgdb.cn/item/6743339788c538a9b5bb66ff.png)

## Hexo文章
### 添加文章
#### 通过Bash
Hexo的新文章通常在Bash中用
```
hexo n type "name"
```
来创建，请看以下例子：<br/>我要创建一个名为`低成本高效率使用Vercel&Github后期运维内容`的`文章`，需要输入
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

我上面所介绍的这些内容有关于你的网站展示在用户前的相貌以及竞价排名，所以请务必认真填写。当然，如果你和我一样不在意SEO,基本上是给自己看，最后两者可以不填，因为它们不会直接在网站上显示出来。剩余的便是主题自带或者Hexo的扩展项，暂时不详细展开，也可以直接跳到。
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
## NexT主题扩展项
> 2024年11月25日更新


在`/themes/hexo-theme-next/_config.yml`我们找到这一部分
```
# ---------------------------------------------------------------
# External Libraries
# See: https://theme-next.js.org/docs/third-party-services/external-libraries
# ---------------------------------------------------------------

# Easily enable fast Ajax navigation on your website.
# For more information: https://github.com/next-theme/pjax
pjax: true

# FancyBox is a tool that offers a nice and elegant way to add zooming functionality for images.
# For more information: https://fancyapps.com/fancybox/
fancybox: true

# Medium Zoom is a JavaScript library for zooming images like Medium.
# Warning: Do not enable both `fancybox` and `mediumzoom`.
# For more information: https://medium-zoom.francoischalifour.com
mediumzoom: false

# Vanilla JavaScript plugin for lazyloading images.
# For more information: https://apoorv.pro/lozad.js/demo/
lazyload: true

# Automatically insert whitespace between CJK and half-width characters.
# For more information: https://github.com/vinta/pangu.js
# Server-side plugin: https://github.com/next-theme/hexo-pangu
pangu: true

# Prefetch links based on what is in the user's viewport.
# For more information: https://getquick.link
# Front-matter variable (nonsupport home archive).
quicklink:
  enable: true

  # Home page and archive page can be controlled through home and archive options below.
  # This configuration item is independent of `enable`.
  home: true
  archive: true

  # Default (true) will initialize quicklink after the load event fires.
  delay: true
  # Custom a time in milliseconds by which the browser must execute prefetching.
  timeout: 3000
  # Default (true) will attempt to use the fetch() API if supported (rather than link[rel=prefetch]).
  priority: true
```
建议修改成上方代码块里的内容，详细解释可以看该系列的下一篇文章。