---
title: 华师大数据学院夏令营项目总结
date: 2023-07-02 17:30
img: http://rx4hz3911.hd-bkt.clouddn.com/src=http%20__c-ssl.duitang.com_uploads_item_201804_28_20180428115829_mpivy.thumb.1000_0.jpg&refer=http%20__c-ssl.duitang.webp
top: true
summary: 本文是对此次华师大数据学院夏令营的总结分享，通过hexo+github搭建个人博客
categories: 经验分享
tags:
- hexo
---

## 博客主题及其选取原因

### 为什么选择hexo框架？

选取hexo作为博客框架的原因之一是因为我本身对node.js有一定了解，也有基于javascript的网页开发经验，对于初接触静态博客来说，hexo是最适合我的了。且hexo也有许多漂亮的主题可供选择，使用命令安装插件也较为容易。

### 为什么选择matery主题

我在hexo官方提供的多个主题中选择了matery(注：之前尝试了几种不同的主题，但是要么是界面过于简略，要么是安装时出现依赖问题，所以也花了不少时间)，事实证明我选对了，这是我体验下来最不错的主题，我也想推荐给大家使用。

matery主题集成了静态博客里主流的功能，配置灵活，有些相同的功能也提供了多种方案可供选择。该主题灵活的交互动画也确实让其增加了不少

作者在主题目录下的`_config.yml`的每一个配置项上都注释标明了相应，甚至对部分功能的配置提供了一些建议，这让我在后续博客功能的添加和修改上确实省下了不少力气。整个主题没有什么硬编码的部分，功能的配置几乎完全集成在`_config.yml`中，当然，`_config.yml`中还可以自己配置需要运行的js脚本，如果想修改外观，主题中还提供了可供自己修改的css文件，这样高灵活度的主题对于想要各种尝试的人确实非常合适。

## 博客页面布局及其设计思路

博客大致分为五个模块，包括首页，标签，分类，归档，关于五个部分。

### 首页

巨幕，包含名言和个人的联系方式，下拉后可以看到文章

![](http://rx4hz3911.hd-bkt.clouddn.com/image-20230702202757433.png)

![](http://rx4hz3911.hd-bkt.clouddn.com/image-20230702204734571.png)

### 标签

可视化展示当前博客的标签数

![](http://rx4hz3911.hd-bkt.clouddn.com/image-20230702205624164.png)

### 分类

可视化展示当前博客的类数

![](http://rx4hz3911.hd-bkt.clouddn.com/image-20230702205723269.png)

### 归档

以时间线和日历展示文章

![](http://rx4hz3911.hd-bkt.clouddn.com/image-20230702205813779.png)

### 关于

展示自己，以及文章统计

![](http://rx4hz3911.hd-bkt.clouddn.com/image-20230702210058003.png)

### 其他功能

音乐播放（左下角），搜索（右上角），留言板（右下角）

<img src="http://rx4hz3911.hd-bkt.clouddn.com/image-20230704150942854.png" alt="image-20230704150942854" style="zoom:50%;" />



<img src="http://rx4hz3911.hd-bkt.clouddn.com/image-20230704144730839.png" alt="image-20230704144730839" style="zoom: 35%;" />

<img src="http://rx4hz3911.hd-bkt.clouddn.com/image-20230704144832190.png" alt="image-20230704144832190" style="zoom:50%;" />

## 博客功能实现及其技术选择
- 本博客的项目结构如下所示：

```bash
├── _config.yml	    #站点配置文件
├── db.json            #缓存文件
├── debug.log       #hexo s --debug 产生的日志文件
├── node_modules    #nodejs 本地包
├── package.json    #nodejs 本地配置信息
├── public               #生成的静态文件所在的文件夹
├── scaffolds          #新生成page的模板
├── source             #文章所在文件夹
|	├──_posts		   #文章存放处
└── themes           #主题所在文件夹
```

- 本博客所用的包信息如下所示：


```bash
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "build": "hexo generate",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "hexo server"
  },
  "hexo": {
    "version": "6.3.0"
  },
  "dependencies": {
    "hexo": "^6.3.0",
    "hexo-deployer-git": "^4.0.0",
    "hexo-generator-archive": "^2.0.0",
    "hexo-generator-category": "^2.0.0",
    "hexo-generator-index": "^3.0.0",
    "hexo-generator-search": "^2.4.3",
    "hexo-generator-tag": "^2.0.0",
    "hexo-renderer-ejs": "^2.0.0",
    "hexo-renderer-marked": "^6.0.0",
    "hexo-renderer-stylus": "^3.0.0",
    "hexo-server": "^3.0.0",
    "hexo-theme-landscape": "^1.0.0",
    "hexo-wordcount": "^6.0.1"
  }
}
```
- 本博客所有图片存储在`七牛云`（官网：https://portal.qiniu.com）存储服务器上


### 搜索功能

搜索功能安装hexo官方插件`hexo-generator-search`，并在`_config.yml`文件中进行配置

```bash
search:
  path: search.xml
  field: post
```

### 留言板功能

留言板使用DaoVoice插件（官网：http://dashboard.daovoice.io）

这需要在其官网注册一个账号并获取app_id，在主题中的`_config.yml`文件中进行配置。

```bash
daovoice:
  enable: true
  app_id: 651b562f
```


### 统计功能

字数统计使用的是官方插件`hexo-wordcount`，浏览人数使用的是busuanzi插件（官网：http://ibruce.info/2015/04/04/busuanzi/）

### 博客制作过程中遇到的问题及其解决方法

在完成这个项目时遇到的问题并不是很多，在完成博客的时候我考虑到一些过程中可以优化的地方。

- 一个是在编写markdown文章时难免会出现插入大量图片的情况，每次插入都需要去关心图片的地址会非常麻烦，使用图床时还需要上传。这里的解决方案是下载PicGo自动化工具和markdown编辑器Typora。Typora能够配置图片插入时的动作，搭配PicGo可以在插入时自动上传到图床且插入正确的图片地址。基于以上，我在截图插入markdown时会自动上传至图床并反馈正确的地址，在编写文档时节省了不少时间。


- 另一个是能够在提交main分支的同时自动部署博客到Github Pages。这里我使用的是Github Actions功能，使用该功能需要配置仓库的公钥和私钥。因为是第一次使用这个功能，尝试了几次都失败了，原因是nodejs依赖配置出现了问题。在`.github`目录下workflows下编写`deploy.yml`即可，代码如下：

  ```bash
  # Action 的名字
  name: Hexo Auto Deploy
  
  on:
    # 触发条件1：main 分支收到 push 后执行任务。
    push:
      branches:
        - main
  
  # 这里放环境变量
  env:
    # Hexo 编译后使用此 git 用户部署到 github 仓库
    GIT_USER: DhuShen
    # Hexo 编译后使用此 git 邮箱部署到 github 仓库
    GIT_EMAIL: massd2002@163.com
    # Hexo 编译后要部署的 github 仓库
    GIT_DEPLOY_REPO: dhushen/dhushen.github.io
    # Hexo 编译后要部署到的分支
    GIT_DEPLOY_BRANCH: pages
  
    # 注意替换为你的 GitHub 源仓库地址
    GIT_SOURCE_REPO: git@github.com:dhushen/dhushen.github.io.git
  
  jobs:
    build:
      name: Build on node ${{ matrix.node_version }} and ${{ matrix.os }}
      runs-on: ubuntu-latest
      if: github.event.repository.owner.id == github.event.sender.id
      strategy:
        matrix:
          os: [ubuntu-18.04]
          node_version: [18.x]
  
      steps:
        - name: Checkout
          uses: actions/checkout@v2
  
        - name: Checkout deploy repo
          uses: actions/checkout@v2
          with:
            repository: ${{ env.GIT_DEPLOY_REPO }}
            ref: ${{ env.GIT_DEPLOY_BRANCH }}
            path: .deploy_git
  
        - name: Use Node.js ${{ matrix.node_version }}
          uses: actions/setup-node@v1
          with:
            node-version: ${{ matrix.node_version }}
  
        - name: Configuration environment
          env:
            HEXO_DEPLOY_PRI: ${{secrets.HEXO_DEPLOY_PRI}}
          run: |
            sudo timedatectl set-timezone "Asia/Shanghai"
            mkdir -p ~/.ssh/
            echo "$HEXO_DEPLOY_PRI" > ~/.ssh/id_rsa
            chmod 600 ~/.ssh/id_rsa
            ssh-keyscan -t rsa github.com >> ~/.ssh/known_hosts
            ssh-keyscan -t rsa e.coding.net >> ~/.ssh/known_hosts
            git config --global user.name $GIT_USER
            git config --global user.email $GIT_EMAIL
  
        - name: Install dependencies
          run: |
                 npm install hexo-cli -g
                 npm install
                 npm install hexo-generator-index2 hexo-symbols-count-time hexo-blog-encrypt hexo-deployer-git hexo-generator-search hexo-wordcount --save
  
        - name: Deploy hexo
          run: |
            npm run deploy
  
  ```

  对main分支git push后可以发现博客自动部署上去了

  ![](http://rx4hz3911.hd-bkt.clouddn.com/image-20230704160905662.png)

## 总结

之前就看到网上的各个程序员大佬都有自己的博客，但是之前也没有去了解怎么实现的。也很感谢夏令营的这次机会让我搭建了一个个人博客，这对我来说是一个契机。这次项目也让我感受到了开源的魅力，如果没有这些有用的开源插件以及GitHub的相关工具，恐怕很难做到这个效果吧。
