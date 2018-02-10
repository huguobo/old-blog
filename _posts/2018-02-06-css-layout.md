---
layout: post
title: FE前端入门系列-三栏布局
date: 2018-02-06 16:50:00
type: css
---

> 简单的三栏布局实现。





## 绝对定位布局

容易理解，上手简单。左中右三个div顺序可以调整，能够让主要内容优先加载。

缺点是中间区域有最小宽度限制，当宽度小于一定程度会发生重叠的情况。

[实例代码](http://jsbin.com/wupoguh/9/edit?html,css,output)

## 流体布局float

代码足够简单

不足之处是中间的容器会受`clear:both`属性的影响。而且div顺序不能改变，无法有限加载重要的内容。

[实例代码](http://jsbin.com/conukuc/1/edit?html,css,output)

## 负Margin

这种布局也叫**双飞翼布局**。首先，中间的主体要使用双层标签。外层`div`宽度`100%`显示，并且浮动（本例左浮动，下面所述依次为基础），内层`div`为真正的主体内容，含有左右`210`像素的`margin`值。左栏与右栏都是采用`margin`负值定位的，左栏左浮动，`margin-left`为`-100%`，由于前面的div宽度100%与浏览器，所以这里的`-100%` `margin`值正好使左栏`div`定位到了页面的左侧；右侧栏也是左浮动，其`margin-left`也是负值，大小为其本身的宽度即`200`像素。

[实例代码](https://jsbin.com/cobice/1/edit?html,css,output)



待更新。。。

### Flex

### Table

### BFC

[什么是BFC](https://www.jianshu.com/p/fc1d61dace7b)







