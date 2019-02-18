---
title: "4-hugo完善LeaveIt小功能"
date: 2019-02-17T23:00:36+08:00
lastmod: 2019-02-17T23:13:36+08:00
draft : false
tags : ["hugo"]
categories : ["hugo"]
type : ["archives"]
---
# 4-hugo完善LeaveIt小功能

&emsp;&emsp;通过前两篇文章介绍，博客功能基本上已经够用了，但是在看了不少博客后，发现，还有一些小功能很有意思，下面就简单配置下。

- ***如下操作都是基于LeaveIt主题进行的***

1. 添加字数统计

    1.1 打开文件 themes\LeaveIt\layouts\_default\single.html，在 22 行后插入一行 DOM：(.WordCount这行)
      
    ```html
    <span class="post-category">
                            {{ range . }}
                            {{- $name := . -}}
                            {{- with $.Site.GetPage "taxonomy" (printf "categories/%s" $name) | default ($.Site.GetPage "taxonomy" (printf "categories/%s" ($name | urlize))) -}}
                              <a href="{{ .Permalink }}"> {{ $name }} </a>
                            {{ end -}}
                            {{ end }}
                    </span>
                    {{- end }}
    				<span class="post-word-count">, {{ .WordCount }} words</span>
    ```
        
2. 添加修改时间

    2.1每篇文件头添加一行修改时间 :lastmod
       
    ```yml
    date: 2019-02-17T23:00:36+08:00
    lastmod: 2019-02-17T23:00:36+08:00
    ```

    2.2 打开文件 themes\LeaveIt\layouts\_default\single.html，在创建时间的代码后，加上如下DOM:
                  
    ```html
        <span class="post-time">
                    updateAt <time datetime={{ dateFormat "Jan 2, 2006" .Lastmod }} itemprop="datePublished">{{ dateFormat "Jan 2, 2006" .Lastmod }}</time>
                    </span>
    ```
		
## 之后再发现一些小功能，在补充哈