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

嫌麻烦可以fork一份 https://github.com/aak1247/hexo-theme-one

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


# 版权信息
虽然NEXT主题自带版权信息，但是不太人性化。版权信息居然会出现在tags和category里面。虽然需要自己做一个，能够手动开启关闭的版权信息。

在目录 next/layout/_macro/下添加 my-copyright.swig:

```javascript
{% if page.copyright %}
<div class="my_post_copyright">
  <script src="//cdn.bootcss.com/clipboard.js/1.5.10/clipboard.min.js"></script>

  <!-- JS库 sweetalert 可修改路径 -->
  <script type="text/javascript" src="http://jslibs.wuxubj.cn/sweetalert_mini/jquery-1.7.1.min.js"></script>
  <script src="http://jslibs.wuxubj.cn/sweetalert_mini/sweetalert.min.js"></script>
  <link rel="stylesheet" type="text/css" href="http://jslibs.wuxubj.cn/sweetalert_mini/sweetalert.mini.css">
  <p><span>本文标题:</span><a href="{{ url_for(page.path) }}">{{ page.title }}</a></p>
  <p><span>文章作者:</span><a href="/" title="访问 {{ theme.author }} 的个人博客">{{ theme.author }}</a></p>
  <p><span>发布时间:</span>{{ page.date.format("YYYY年MM月DD日 - HH:MM") }}</p>
  <p><span>最后更新:</span>{{ page.updated.format("YYYY年MM月DD日 - HH:MM") }}</p>
  <p><span>原始链接:</span><a href="{{ url_for(page.path) }}" title="{{ page.title }}">{{ page.permalink }}</a>
    <span class="copy-path"  title="点击复制文章链接"><i class="fa fa-clipboard" data-clipboard-text="{{ page.permalink }}"  aria-label="复制成功！"></i></span>
  </p>
  <p><span>许可协议:</span><i class="fa fa-creative-commons"></i> <a rel="license" href="https://creativecommons.org/licenses/by-nc-nd/4.0/" target="_blank" title="Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)">署名-非商业性使用-禁止演绎 4.0 国际</a> 转载请保留原文链接及作者。</p>  
</div>
<script> 
    var clipboard = new Clipboard('.fa-clipboard');
    clipboard.on('success', $(function(){
      $(".fa-clipboard").click(function(){
        swal({   
          title: "",   
          text: '复制成功',   
          html: false,
          timer: 500,   
          showConfirmButton: false
        });
      });
    }));  
</script>
{% endif %}
```

在目录next/source/css/_common/components/post/下添加my-post-copyright.styl：
```js
.my_post_copyright {
  width: 85%;
  max-width: 45em;
  margin: 2.8em auto 0;
  padding: 0.5em 1.0em;
  border: 1px solid #d3d3d3;
  font-size: 0.93rem;
  line-height: 1.6em;
  word-break: break-all;
  background: rgba(255,255,255,0.4);
}
.my_post_copyright p{margin:0;}
.my_post_copyright span {
  display: inline-block;
  width: 5.2em;
  color: #b5b5b5;
  font-weight: bold;
}
.my_post_copyright .raw {
  margin-left: 1em;
  width: 5em;
}
.my_post_copyright a {
  color: #808080;
  border-bottom:0;
}
.my_post_copyright a:hover {
  color: #a3d2a3;
  text-decoration: underline;
}
.my_post_copyright:hover .fa-clipboard {
  color: #000;
}
.my_post_copyright .post-url:hover {
  font-weight: normal;
}
.my_post_copyright .copy-path {
  margin-left: 1em;
  width: 1em;
  +mobile(){display:none;}
}
.my_post_copyright .copy-path:hover {
  color: #808080;
  cursor: pointer;
}
```

修改next/layout/_macro/post.swig，在代码
```html
<div>
      {% if not is_index %}
        {% include 'wechat-subscriber.swig' %}
      {% endif %}
</div>
```
之前添加增加如下代码：
```html
<div>
      {% if not is_index %}
        {% include 'my-copyright.swig' %}
      {% endif %}
</div>
```

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
