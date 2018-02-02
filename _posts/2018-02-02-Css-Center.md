---

layout: post
title: FE前端入门系列-CSS垂直居中
date: 2018-02-02 16:50:00
type: css
comment: y

---

# FE前端入门系列-CSS垂直居中

> css居中在实际项目中会平凡的使用到，根据实际场景使用的方案也不尽相同，总结一下。
>
> 下文中我们用容器元素代表外层元素，子元素代表内层元素，即需要居中的元素。







### 方案一 :`margin:auto`

在明确容器元素的宽高和边界的情况下。子元素设置为绝对定位`position:absolute`结合`margin:auto`实现。

[代码示例](https://jsbin.com/giqukov/1/edit?html,css,output)

### 方案二：table布局

不需要明确居中元素的宽高,兼容IE8。

需要有2个container，table table-cell 以及子元素inline-block的处理方式。为什么使用inline-block：块级元素宽度会自动填满父元素，inline-block会由内容撑开。

1. 容器元素：display: table；
2. 居中元素：display: table-cell + vertical-align: middle实现垂直居中

[代码示例](https://jsbin.com/yezikav/1/edit?html,css,output)

###  方案三： Flex

Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。 

Flex使用方便，及其灵活。但是不兼容IE8, 移动端Android4.2一下版本支持不好。

1、主轴居中：content-justify：center

2、交叉轴居中：align-items: center

关于flex的学习参考[阮一峰老师的教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

还有这个[flex小游戏](http://flexboxfroggy.com/)

### 方案四：line-box

这种方法兼容性较好，不需要明确居中元素的宽高。但是需要额外的伪元素，且原理不易理解。

通过一个inline-block伪元素将line box的高度撑到整屏高度。

给伪元素设置`vertrical-align:middle`使得父元素的字体的中心与伪元素的中线对齐。

将居中元素设置为`inline-block`，利用`vertrical-align:middle`进行垂直居中。

[关于伪元素和伪类](http://www.alloyteam.com/2016/05/summary-of-pseudo-classes-and-pseudo-elements/#prettyPhoto)

[查看实例代码](http://jsbin.com/yisehi/2/edit?html,css,output)

### 方案五：绝对定位和transform

1. 通过绝对定位将居中元素的左上角移动到包含块的中心

（top, left: 偏移的百分比是来自包含块的height和wdith）

2. 再利用`transform将**居中元素**的中心与**容器元素**的中心对齐`

这种方法不需要明确居中元素的宽高，不兼容IE8

[查看实例代码](http://jsbin.com/jucusih/edit?html,css,output)

### 方案六：负margin和绝对定位实现

1. 通过绝对定位将居中元素的左上角移动到包含块的中心

（top, left: 偏移的百分比是来自包含块的height和wdith）

2. 通过负margin将居中元素

这种方法需要明确居中元素的宽高，方法简单，可以结合使用calc使用。

[查看示例代码](http://jsbin.com/xesikus/1/edit?html,css,output)



不管是哪种居中方案，都有其优点和弊端，需结合实际场景进行选择和使用。