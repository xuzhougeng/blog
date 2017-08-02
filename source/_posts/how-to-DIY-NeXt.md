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

嫌麻烦可以fork一份 https://github.com/aak1247/hexo-theme-one 然后在此基础上进行修改。


## 修改`_config.yml`
要修改的内容如下：
```
keywords:
menu: 选择你自己需要的，不需要的用#注释掉
  home: /
  categories: /categories
  #about: /about
  archives: /archives
  tags: /tags
  #issue: /issue
  #works: /works
  sitemap: /sitemap.xml
  #commonweal: /404.html
social: #替换成自己的地址
Blogrolls: # 按需修改 
leancloud_visitors: 
  enable: false

# 在source/images/ 下替换成合适的图片
reward_comment: "觉得有用的话赞助一点吧~"
wechatpay: /images/wechatpay.png
alipay: /images/alipay.jpg
```
另外注释掉所有和多说有关的信息

上面几步做完之后，页面就挺好看的啦，后面在进行个性化的定制。


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
