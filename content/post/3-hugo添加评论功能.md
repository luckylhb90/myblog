---
title: "3-hugo添加评论功能"
date: 2019-02-17T10:29:36+08:00
lastmod: 2019-02-17T22:29:36+08:00
draft : false
tags : ["hugo"]
categories : ["hugo"]
type : ["archives"]
---
# hugo添加评论功能
上篇文章，搭建好了基础的github pages，现在基本可以正常使用了，剩下的就是修修补补，添加下可用插件了，目前考虑先整合个评论插件，通过google，发现现使用较多有disqus Gitment valine gittalk。其他评论插件可参考下文连接，总结的相当多，真是牛逼啊。
> https://blog.shuiba.co/comment-systems-recommendation

> disqus 说是需要翻墙才可使用    
> Gitment 可能存在安全问题    
> gittalk 和gitment差不多   
> valine 貌似也不错，之后考虑加上   

综上分析，最后我选择了utterances，发现这个配置真心简单啊。。。

> 参考了该博文，https://mogeko.github.io/2018/025/    
> 虽然文中用的是gittalk，但是方法基本一样。

## huho配置utterances

- ***如下操作都是基于LeaveIt主题进行的***

1. 打开themes\LeaveIt\layouts\_default\single.html
2. 修改post-comment为如下代码，主要是!-- Comments --下面这行

    ```html
    <div class="post-comment">
          {{ if ( .Params.showComments | default true ) }}
                 {{ if ne .Site.DisqusShortname "" }}
                     {{ template "_internal/disqus.html" . }}
                 {{ end }}
          {{ end }}
		  <!-- Comments -->
		  {{ partial "comments.html" . }}
    </div>
    ```

3. 然后在themes\LeaveIt\layouts\partials下建立一个comments.html文件，填入如下代码

    ```html
  <!-- utterances -->
  {{- if .Site.Params.utterances.owner}}
	<div class="post bg-white">
		<script src="https://utteranc.es/client.js"
			  repo="{{ .Site.Params.utterances.owner }}/{{ .Site.Params.utterances.repo }}"
			  issue-term="{{ .Site.Params.utterances.issueTerm }}"
			  theme="{{ .Site.Params.utterances.theme }}"
			  crossorigin="anonymous"
			  async>
		</script>
		<noscript>Please enable JavaScript to view the <a href="https://github.com/utterance">comments powered by utterances.</a></noscript>
	</div>
  {{- end }}
    ```

4. 配置 config.toml

    ```yml
[params.utterances]         # utteranc is a comment system based on GitHub issues. see https://utteranc.es
    owner = "xxxx" # github用户名
    repo = "yyyy"    # 仓库地址The repo to store comments
    issueTerm = "pathname"	
	theme = "github-light"
    ```

5. github建立一个上文配置的仓库地址即可


## 参考
> https://blog.shuiba.co/comment-systems-recommendation      
> https://mogeko.github.io/2018/025/
> https://utteranc.es/?installation_id=676028&setup_action=install