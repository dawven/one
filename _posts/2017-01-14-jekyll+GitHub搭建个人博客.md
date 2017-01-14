---
layout: post
title: "jekyll+GitHub搭建个人博客"
date: 2017-01-14 
description: "HEXO配置，jekyll+Github，搭建自己的博客"
tag: 博客 
---   

　　经过各种找资料，踩过各种坑，终于使用 jekyll 搭建个人博客初步完成了，域名我买了一个，很便宜，一块钱一年，把域名解析到与我GitHub关联。利用Github提供的Pages功能，把本地搭建的Jekyll站点部署上去，实现一个自由定制的个人静态博客。效果还不错，[博客模板效果](http://viento.xyz/#blog)

 

## 正文：
　

　之前是想着写博客，一方面是给自己做笔记，可以提升自己的写作、总结能力，一个技术点我们会使用，并不难，但是要做到让让别人也能听懂我们讲得，还是需要一定的技巧和经验的。很多类似于CSDN、博客园也都可以写文章，但是页面的样式我，不是太喜欢。最近看到一些大神们的博客，我也依葫芦画瓢的搭建了一个。打算以后就在这写东西了，虽然微信公众号我也没什么理过，先感谢大家厚爱。微信公众号以后可能还是会写写的。

Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过Markdown （或者 Textile） 以及 Liquid 转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的

　使用 Jekyll 搭建博客之前要确认下本机环境，Git 环境（用于部署到远端）、[Ruby](http://www.ruby-lang.org/en/downloads/) 环境（Jekyll 是基于 Ruby 开发的）、包管理器 [RubyGems](http://rubygems.org/pages/download)                
　　如果你是 Mac 用户，你就需要安装 Xcode 和 Command-Line Tools了。下载方式 Preferences → Downloads → Components。

　　Jekyll 是一个免费的简单静态网页生成工具，可以配合第三方服务例如： Disqus（评论）、多说(评论) 以及分享 等等扩展功能，Jekyll 可以直接部署在 Github（国外） 或 Coding（国内） 上，可以绑定自己的域名。[Jekyll中文文档](http://jekyll.bootcss.com/)、[Jekyll英文文档](https://jekyllrb.com/)、[Jekyll主题列表](http://jekyllthemes.org/)。
 
## 配置环境     

### Jekyll 环境配置

安装 jekyll

```     
$ gem install jekyll     
```    

创建博客

```    
$ jekyll new myBlog    
```   

进入博客目录

```
$ cd myBlog  
```

启动本地服务

```
$ jekyll serve
```

在浏览器里输入： [http://localhost:4000](http://localhost:4000)，就可以看到你的博客效果了。

![](/images/posts/jekyll/image1.png)

so easy !

### 目录结构
　
　Jekyll 的核心其实是一个文本转换引擎。它的概念其实就是： 你用你最喜欢的标记语言来写文章，可以是 Markdown，也可以是 Textile,或者就是简单的 HTML, 然后 Jekyll 就会帮你套入一个或一系列的布局中。在整个过程中你可以设置URL路径, 你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的静态页面就是你的成品了。

 一个基本的 Jekyll 网站的目录结构一般是像这样的：

```
.
├── _config.yml
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   ├── post.html
|   └── page.html
├── _posts
|   └── 2016-10-08-welcome-to-jekyll.markdown
├── _sass
|   ├── _base.scss
|   ├── _layout.scss
|   └── _syntax-highlighting.scss
├── about.md
├── css
|   └── main.scss
├── feed.xml
└── index.html

```

这些目录结构以及具体的作用可以参考 [官网文档](http://jekyll.com.cn/docs/structure/) 

进入 _config.yml 里面，修改成你想看到的信息，重新 jekyll server ，刷新浏览器就可以看到你刚刚修改的信息了。

到此，博客初步搭建算是完成了，

### 博客部署到远端 

　我这里讲的是部署到 Github Page 创建一个 github 账号，然后创建一个跟你账户名一样的仓库，如我的 github 账户名叫 [pangkanghua](https://github.com/pangkanghua)，我的 github 仓库名就叫 [pangkanghua.github.io](https://github.com/pangkanghua/pangkanghua.github.io)，创建好了之后，把刚才建立的 myBlog 项目 push 到 username.github.io仓库里去（username指的是你的github用户名），检查你远端仓库已经跟你本地 myBlog 同步了，然后你在浏览器里输入 username.github.io ，就可以访问你的博客了。


### 编写文章

　　所有的文章都是 _posts 目录下面，文章格式为 mardown 格式，文章文件名可以是 .mardown 或者 .md。

　　编写一篇新文章很简单，你可以直接从 _posts/ 目录下复制一份出来 `2016-10-16-welcome-to-jekyll副本.markdown` ，修改名字为 2016-10-16-article1.markdown ，注意：文章名的格式前面必须为 2016-10-16- ，日期可以修改，但必须为 年-月-日- 格式，后面的 article1 是整个文章的连接 URL，如果文章名为中文，那么文章的连接URL就会变成这样的：http://baixin.io/2015/08/%E6%90%AD%E5/ ， 所以建议文章名最好是英文的或者阿拉伯数字。 双击 2016-10-16-article1.markdown 打开

```

---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-10-16 11:29:08 +0800
categories: jekyll update
---

正文...

```


title: 显示的文章名， 如：title: 我的第一篇文章                    
date:  显示的文章发布日期，如：date: 2016-10-16                          
categories: tag标签的分类，如：categories: 随笔            

注意：文章头部格式必须为上面的，.... 就是文章的正文内容。

我写文章使用的是 Sublime Text3 编辑器，如果你对 markdown 语法不熟悉的话，可以看看[作业部落的教程](https://www.zybuluo.com/) 
对于小白可能表述不清，出现很多问题，推荐大家去百度，我也会贴个人觉得很好的教程
[Jekyll和Github搭建个人静态博客](http://pwnny.cn/original/2016/06/26/MakeBlog.html)
[Jekyll搭建个人博客(我的主题就是借他的)](http://baixin.io/2016/10/jekyll_tutorials1/)
[使用 github + jekyll 搭建个人博客](http://www.cnblogs.com/wangfupeng1988/p/5702324.html)
