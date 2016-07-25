---
layout: post
title: 解决jekyll博客加载慢的问题
date: 2016-05-10 15:27:31

---
##解决jekyll博客加载慢的问题
>经过好长时间的折腾，在windows下配置好了*jekyll*，配合上自己的*github for windows*。环境上算弄好了，不得不说在windows系统装他们还是蛮艰辛的，之后会整理一下安装过程中需要注意的问题和需要下载的工具发布出来。

调试时发现，不论是本地用jekyll服务从**127.0.0.1：4000**端口访问还是从托管在github上的huguobo.github.io上访问都加载的异常的慢。应该不是结构优化上的问题啊，因为博客基本还啥都没有呢。后来看到了css和js引用的中的google的大字，但是他们的确需要啊，只能说在天朝都懂。

##CSS font.google 本地化
既然是google服务器在本地有限制，那么要不从代理或者浏览器方面出发，要不就下载个本地的吧，毕竟是个小博客~~，去这个网址（访问还是能访问到的，就是加载慢），复制内容，粘贴到本地文件，命名为google.css。<br>
 `<link href='http://fonts.googleapis.com/css?family=Open+Sans:400,700' rel='stylesheet' type='text/css' />`<br/>
替换为
 `<link href='{{ site.url }}/stylesheets/google.css' rel='stylesheet' type='text/css' />`
即可
##jsapi 后置
`<script type="text/javascript" src="https://www.google.com/jsapi"></script>`<br/>
这句话是加载慢的罪魁祸首，因为单纯的我把他放在head标签里了。我们也可以去google下载到这个js文件然后用和上面相似的办法，但是这个文件有点大，我不想下载（哈哈哈哈哈哈）。于是把他移动到body结束的后面加载即可，先加载有用的显示出来呗~~~





