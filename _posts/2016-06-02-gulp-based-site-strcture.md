---
layout: post
title: 基于gulp前端静态站点结构
date: 2016-06-02 19:30:31
comment: y
---
###简介：
我们使用gulp来处理静态资源文件，通常将处理好的文件生成到一个新的文件夹，也许会有这么一个疑问，既然都生成到新的文件夹里了，那页面引用不是乱套了？<br/>




####1、概述
1.1、本文基于静态站点分离结构所写<br/>
1.2、通过gulp打包好(压缩、合并等操作)资源，通常会生成到新的一个文件夹内。像这样：<br/>
![glup1](http://static.ydcss.com/uploads/2015/10/static-01.png)

---
####2、结合gulp静态资源分离实现的目的
2.1、将静态资源（img、js、css等跟程序部分完全分离），有利于处理CDN加速<br/>
2.2、方便在未打包和已打包资源切换调试，开发时当然不希望代码是压缩的<br/>
2.3、源码部分不想发布至线上，比如sass/less文件是不必放到线上的<br/>
2.4、……
---
####3、开发时和线上的状态（后面的路径都是保持一致，只是站点路径不相同而已）
![gulp2](http://static.ydcss.com/uploads/2015/10/static-02.png)
**注：通常我们的页面都不是纯html，假设页面为php页面（所以让程序帮弄个配置，或者其他办法）实际上页面应该是这样的↓↓↓↓↓：**<br/>
![gulp3](http://static.ydcss.com/uploads/2015/10/static-03.png)

3.1$this->config->item('domain_static');是读取配置文件，只要修改对应值，就可以切换源码和发布后的代码。相当于有一个开关，控制是开发阶段还是测试阶段。<br/>
例如：domain_static值为http://192.168.61.169:1111/则为开发源码，改为http://192.168.61.169:2222/则为发布代码，当然，线上domain_static值为http://static.ydcss.com/<br/>
3.2大家可以根据实际情况，灵活改变即可。

---
####4、结束语
4.1、本文有任何错误，或有任何疑问，欢迎留言说明。