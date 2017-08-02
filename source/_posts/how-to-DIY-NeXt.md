---
title: 如何配置NexT主题
date: 2017/7/31
updated: 2017/8/2
comments: true
categories:
- 'Hexo'
tags:
- "Hexo"
---

折腾了半天，终于标签和分类能用了。
<!--more-->


# 生成标签和分类
利用travis-ci自动部署时，需要自己在blog仓库中添加标签和分类文件。
也就是
```
source/
  _posts/your-blog.md
  categories/index.md
  tags/index.md
```
然后index.md内容如下
```
---
title: 分类
date: 2017-07-31
type: "categories"
comments: false
---

```
把titile和type做相应的修改就行。


# 留言板
如果没有人在博客下留言， 就真的应了那句话，“所谓博客，就是孤芳自赏了”。 由于多说不干了，网易云跟帖也要关闭服务了，于是就只能用disqus（要翻墙）了。
修改配置文件的disqus为true， 然后你还需要注册disqus，获取shortname
```
disqus:
  enable: true
  shortname:
  count: true
```

# 谷歌分析
既然都要翻墙，不如再来一个谷歌分析吧。获取跟踪ID，一般是UA-xxxx
```
Google Analytics
google_analytics:
```


# 内容分享
这个很简单
```
baidu_push: true
```

# 搜索服务
在.travis.yml里的before_install中添加
```
npm install hexo-generator-searchdb --save
```

然后在站点配置文件（也就是blog）中添加如下
```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```
然后在主题配置文件里启用
```
local_search:
  enable: true
```



# 美化页面
关于hexo主题的美化，其实已经有很多文章了，所以下面就列举我参考过的网站
- https://ijiaober.github.io/categories/hexo/
- http://theme-next.iissnan.com/theme-settings.html
- http://blog.csdn.net/qq_33699981/article/details/72716951
