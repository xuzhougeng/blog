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


# 留言板
如果没有人在博客下留言， 就真的应了那句话，“所谓博客，就是孤芳自赏了”

第一步， 在主题文件下的 `_config.yml` 添加message标识
```
menu:
  home: /
  categories: /categories
  #about: /about/
  archives: /archives
  tags: /tags
  sitemap: /sitemap.xml
  message: /message
  #commonweal: /404.html
menu_icons:
  enable: true
  #KeyMapsToMenuItemKey: NameOfTheIconFromFontAwesome
  home: home
  about: user
  categories: th
  schedule: calendar
  tags: tags
  archives: archive
  sitemap: sitemap
  message: comment
  commonweal: heartbeat
```

第二步，在主题文件下`languages/zh-Hans.yml` 添加messge对应的中文
```
menu:
  home: 首页
  archives: 归档
  categories: 分类
  tags: 标签
  about: 关于
  search: 搜索
  schedule: 日程表
  sitemap: 站点地图
  commonweal: 公益404
  message: 互动区
```  

第三步，完善页面
由于多说不干了，网易云跟帖也要退出了，所以就只用github issue实现了

在`next/latout/_custom/`新建一个issue.swig文件， 复制如下内容：
```html
<blockquote class="blockquote-center leave-message">快来留言吧！~请在 <a href="https://github.com/xuzhougeng/xuzhougeng.github.io/issues/1" target="_blank">Github issue</a> 页面完成操作</blockquote>
<div id="messages">
    <div id="gh-comments-info">
            <a href="javascript:void(0) ;">
            <span id="gh-comments-count">0</span>条留言</a>
    </div>
    <div id="gh-comments" style="opacity: 1"></div>
</div>
<script src="https://cdn.jsdelivr.net/jquery/2.1.3/jquery.min.js"></script>
<script type="text/javascript" src="{{ url_for(theme.js)  }}/src/issue.js"></script>
```

然后在layout/page.swig里面做如下修改
```
div id="posts" class="posts-expand">
...
{{ page.content }}
{% elif page.type === 'issue' %}
{% include '_custom/issue.swig' %}
{% endif %}
```

然后你还需要在source下建立message文件，在里面添加`index.md`
```
---
title: 互动区
date: 2017-07-01
type: "issue"
comments: false
---
```

太复杂了，感冒中，未完待续



# 美化页面
关于hexo主题的美化，其实已经有很多文章了，所以下面就列举我参考过的网站
- https://ijiaober.github.io/categories/hexo/
- http://theme-next.iissnan.com/theme-settings.html
- http://blog.csdn.net/qq_33699981/article/details/72716951
