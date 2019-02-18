---
title: "2-hugo搭建github-pages"
date: 2019-02-16T22:15:36+08:00
lastmod: 2019-02-16T22:15:36+08:00
draft : false
tags : ["hugo"]
categories : ["hugo"]
type : ["archives"]
---
# hugo 搭建github page

&emsp;&emsp;最近心血来潮，突然想继续写写博客，提高下写作文的水平（上学期间，作文就没写够过800字，尴尬啊）。

&emsp;&emsp;然后最近就研究了下github page，google下，发现比较流行的三个静态页面生成框架，jekyll hexo hugo。
简单做了下对比：

框架 | 语言 | 性能 |模板|搭建成本
------|------|------|------|------
jekyll|ruby|慢|够用|较简单
hexo|nodejs|比较快|够用|麻烦
hugo|go|快|够用|简单

&emsp;&emsp;看了实现语言，自己目前多少了解一些go语法，其他两种语言个人了解不多，还有性能方面，看了大部分人的使用情况，发现hugo生成速度最快，所以我最终也选择了该框架。

下面简单说下搭建过程：

#### windows 版本 ：

1. 参考官方文档安装即可：

    > http://www.gohugo.org/doc/tutorials/installing-on-windows/   

2. 安装完成之后，参考该文档生成页面：  

    > http://www.gohugo.org/post/coderzh-hugo/   
> 文中说下载全部模板失败，我这通过一个小时都下载成功了，这样就可以随心所欲换模板了，看了下有1.9G左右，还是不小的。点击图中更新所有子模块，慢慢更新即可。

![2-1](https://luckylhb90.github.io/images/2/2-1.jpg)

> 每个模板中都有一个默认的配置    
> 可以将themes\XXXX\exampleSite\config.toml 拷贝到 hugo新建站点的根目录下，然后在这个基础上修改，相对方便点。

#### 命令简要说明下

> **注意在站点目录下执行**

1. hugo 

    > 直接执行可以生成public目录，这个目录就是最终要上传到github仓库的。

2. hugo server

    > 本地启动服务，可以浏览器直接访问   
> *后面还可添加一些参数*   
> -t XXX(或者--theme=XXX)参数的意思是使用XXX主题渲染我们的页面   
> --buildDrafts参数设置为true，运行Hugo时要加上--buildDrafts参数才会生成被标记为草稿的页面   
> –watch或者-w  选项打开的话，将会监控到文章的改动从而自动去刷新浏览器(现在应该是默认开启的)

#### 问题记录

1. 使用主题时，确保主题已下载到本地.

    > 第一次使用时，指定了一个主题，发现怎么启动都看不到页面，查了半天，发现themes这个主题的目录都是空的，ε(┬┬﹏┬┬)3。。。    

2. md文档头部的+++ 和 --- 都可以使用。但是格式有略微不同。 
    
    ```
+++
draft = false
+++
    ```
    ```
---
draft : false
---
    ```
3. hugo 的markdown语法貌似不太一样，所以参考了如下文档研究了下。 

    > https://blog.pytool.com/language/golang/hugo/hugo_markdown/
> http://blog.baiqp.info/theme-markdown-grammar/

#### 命令使用总结(win&&linux混用，仅做参考记录)
```
cd D:\hugo
mkdir bin
mkdir sites
cd bin && wget https://github.com/spf13/hugo/releases/最新版本
unzip hugo-XXXXXXX.zip
set PATH=%PATH%;D:\hugo\bin
hugo version
cd D:\hugo\sites
hugo new site example.com
cd example.com
hugo new about.md
hugo new post/first.md
git clone --recursive https://github.com/spf13/hugoThemes themes
cp themes\XXXX\exampleSite\config.toml .\
hugo
hugo server

cd public
-- github 新建一个空项目
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/xxxxx/xxxxxx.git
git push -u origin master

```

#### 参考
> http://www.gohugo.org/doc/tutorials/installing-on-windows/    
> http://www.gohugo.org/post/coderzh-hugo/    
> https://jimmysong.io/posts/building-github-pages-with-hugo/    
> https://blog.pytool.com/language/golang/hugo/hugo_markdown/    
> http://blog.baiqp.info/theme-markdown-grammar/    
> https://zhuanlan.zhihu.com/p/37752930    
> https://jimmysong.io/hugo-handbook/    
> https://www.staticgen.com/