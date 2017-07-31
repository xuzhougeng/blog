---
title: 如何配置NexT主题
date: 2017/7/31
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


# 美化页面
关于hexo主题的美化，其实已经有很多文章了，所以下面就列举我参考过的网站
- https://ijiaober.github.io/categories/hexo/
- http://theme-next.iissnan.com/theme-settings.html
- http://blog.csdn.net/qq_33699981/article/details/72716951
