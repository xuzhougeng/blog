---
title: 这个博客是如何搭建的
date: 2017/7/30
tags:
    - Hexo
---

这个博客的搭建之路
## 安装软件
- git: https://git-scm.com/downloads
- node.js: https://nodejs.org/en/
- hexo

```
# git
sudo apt-get install git
# conda install git

# node.js
# use nvm to install node.js
wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
nvm install stable
## add taobao mirrors to speed downloading
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"
# hexo
npm install -g hexo-cli
```

<!--more-->

## 安装软件
- git: https://git-scm.com/downloads
- node.js: https://nodejs.org/en/
- hexo

```
# git
sudo apt-get install git
# conda install git

# node.js
# use nvm to install node.js
wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
nvm install stable
## add taobao mirrors to speed downloading
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"
# hexo
npm install -g hexo-cli
```

检查是否安装成功：
```
hexo -v
# 以下是输出，有内容就行
hexo-cli: 1.0.3                                        
os: Linux 4.4.0-43-Microsoft linux x64                 
http_parser: 2.7.0                                     
node: 8.2.1                                            
v8: 5.8.283.41                                         
uv: 1.13.1                                             
zlib: 1.2.11                                           
ares: 1.10.1-DEV                                       
modules: 57                                            
openssl: 1.0.2l                                        
icu: 59.1                                              
unicode: 9.0                                           
cldr: 31.0.1                                           
tz: 2017b                                              
xzg@DESKTOP-CNF0I9C:~$                                 
```

具体的官方文档： https://hexo.io/docs/ 提供了macOS Linux 和Windows平台的安装方法。


## Hexo建立第一个博客
第一步：在本地新建一个文件夹，初始化hexo:
```
mkdir xuzhougeng
cd xuzhougeng
git init xuzhogueng
```

初始化之后, 会得到如下内容：
```
.
├── _config.yml # 存在网站的配置信息
├── package.json # 存放应用程序信息， 使用npm install 安装
├── scaffolds # 存放模板，
├── source # 存放用户资源
|   ├── _drafts
|   └── _posts
└── themes # 存放主题
```

第二步： 安装应用程序
```
npm install
```

第三步： 发布第一个博客
```
hexo new hello-world.md
# INFO  Created: /mnt/e/xuzhougeng/source/_posts/hello-world-md.md
# 可在里面说些什么，也可以什么都不做
hexo generate
```

第四步： 本地预览
```
hexo server # hexo s
```

![](http://oex750gzt.bkt.clouddn.com/17-7-30/620386.jpg)


## 部署到GitHub Page
如果你有一台服务器，基本上就不需要这一步了。但是服务器实在不便宜，好在有免费的GitHub page给我们用。
再继续之前，建议你去看一下Git的教程：  [http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
还有GitHub Page的介绍：  [https://pages.github.com/](https://pages.github.com/)

反正不管如何，你先得到GitHub上 (https://github.com/) 申请一下账号，然后新建一个托管网页的库
![](http://oex750gzt.bkt.clouddn.com/17-7-30/18924627.jpg)
![](http://oex750gzt.bkt.clouddn.com/17-7-30/66854364.jpg)

如果你上面的git教程没时间看完， 至少把里面的关于远程库的内容看了，保证你的电脑被GitHub认证了。
大致步骤是在本地生成SSH秘钥, 一路回车哦
```
ssh-keygen -t rsa -C "你的邮箱地址"

```
查看本地SSH秘钥，并且复制

```
cat ~/.ssh/id_rsa.pub
```

![](http://oex750gzt.bkt.clouddn.com/17-7-30/77971997.jpg)
借用一下git教程的图，SSH秘钥复制到图中位置。

![](http://oex750gzt.bkt.clouddn.com/17-7-30/34958163.jpg)
之后要安装hexo的git插件
```
cnpm install hexo -server --save
cnpm install hexo-deployer-git --save
```

修改配置文件，增加部署部分
```
# Deployment
## 这里是重点，这里是修改发布地址，因为我们前面已经加了 SSH 密钥信息在 Github 设置里面了，所以只要我们电脑里面持有那两个密钥文件就可以无需密码地跟 Github 做同步。
## 需要注意的是这里的 repo 采用的是 ssh 的地址，而不是 https 的。分支我们默认采用 master 分支，以后你翅膀硬了要换其他也无所谓。
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo:
      github: git@github.com:xuzhougeng/xuzhougeng.github.io.git,master
```

部署到github上
```
hexo clean
hexo generate
# 可选，本地预览
hexo server
# hexo deploy
```

小功告成，保证的远程库下是下面这个样子
![](http://oex750gzt.bkt.clouddn.com/17-7-30/17073006.jpg)

## 优雅的使用Hexo
但是，如果在一台新电脑上使用hexo的时候，还是需要装各种软件。此外如果从GitHub克隆已有库到本地，还不能直接用。根据zccz14的博文[优雅地使用 Hexo](https://zccz14.com/2016/12/30/%E4%BC%98%E9%9B%85%E5%9C%B0%E4%BD%BF%E7%94%A8Hexo/)， 是该用Travis CI自动化部署了。

我们需要两个仓库： 一个命名为username.github.io，一个随意，比如说叫做blog

在[Travis CI](https://travis-ci.org/)上注册并关联GitHub账号。然后在Travis CI中添加对blog对关联。
![](http://oex750gzt.bkt.clouddn.com/17-7-30/94272214.jpg)

然后在Travis CI blog的setting中做如下配置
1. 确保 Build only if .travis.yml is present, Build pushes, Build pull requests 处于打开状态。
2. 增加环境变量： GITHUB_USERNAME: GitHub 的用户名, GITHUB_TOKEN: GitHub 令牌, GITHUB_EMAIL: GitHub 的邮箱, THEME_URI: 主题的URI, THEME_NAME: 主题名



本地对同步GitHub的blog仓库
```
git clone git@github.com:xuzhougeng/blog.git
```

从之前初始化的hexo项目中把`package.json`和`_config.yml`拷贝到同步的仓库中，新建一个`source/_posts/`存放用于发布的文章，复制一份官方博文到该目录下
```
cp _config.yml  package.json ../blog/
# source/_posts 目录下的Markdown文件都会被渲染成文章
mkdir -p source/_posts/
# or
cp -r source/_posts/hello-world.md ../blog/
```

最重要的一步就是在blog下增加`.travis.yml `。这个文件告诉了Travis CI该如何部署。
```
language: node_js
node_js:
    - "6"
before_install:
    - git config --global user.email $GITHUB_EMAIL
    - git config --global user.name $GITHUB_USERNAME
    - npm i hexo-cli -g
    - git clone $THEME_URI themes/$THEME_NAME
script:
    - hexo config theme $THEME_NAME
    - hexo generate
after_success:
    - cd public
    - git init
    - git add .
    - git commit -m "Travis Deploy"
    - git push -f -q https://$GITHUB_TOKEN@github.com/$GITHUB_USERNAME/$GITHUB_USERNAME.github.io master
```

这些都是共性部分，而下面的则是自定义部分。

## 主题分离
在`.travis.yml` 里面`- git clone $THEME_URI themes/$THEME_NAME` 部分就是获取主题所在GitHub地址，然后用`hexo config theme $THEME_NAME` 修改原先的主题。

我这里就先fork别人的主题.于是就需要在traiv CI修改`https://github.com/xuzhougeng/hexo-theme-next`

这是一个非常常用的主题，然后也有很多方案介绍如何修改，修改方案，见 https://zhuanlan.zhihu.com/p/28128674


## 写作
写作就是在`source/_posts/`下新建一个markdown文件，然后在里面以markdown语法进行写作就好了。
唯一比较烦人的问题就是如何处理图片的问题，目前我用的是七牛+极简图床


## 一些小技巧
- 页面内嵌PDF
```
<!--more-->
<iframe src="your_pdf_url" style="width:100%; height:800px"></iframe>
```

- 内嵌网页云音乐
```
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=562010&auto=0&height=66"></iframe>
```
