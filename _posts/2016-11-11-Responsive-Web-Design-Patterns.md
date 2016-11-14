---
layout: post
title: 多设备布局:响应式设计模型一
date: 2016-11-11 22:00:00
type: Responsive-Web-Design-Patterns
comment: y
---

>虽然响应式网页设计样式正在快速发展，但能够完全兼容桌面级设备与移动设备的成熟样式却是屈指可数。

#响应式设计模型
大多数的响应式网页设计可以归纳为五种模式：mostly fluid, column drop, layout shifter, tiny tweaks 和 off canvas。一些情况下，页面可能会采用组合设计模式，例如同时采用 column drop 与 off canvas。 这些样式最初都是由 Luke Wroblewski 定义的，他们为设计响应式式页面提供了一个坚实的基础。





###设计模型

为了创建简洁易懂的示例，下面提到的每一个案例都是基于flexbox通过真实的标签创建的, 主要是在一个主 div内包含三个内容 div。 每个示例都由定义最小视图开始，并在必要的时候加入响应节点（breakpoint）。 flexbox 布局模式 能很好的支持现在的主流浏览，尽管为了最佳效果你可能需要依赖特定的前缀。

###大体流动行模型

Mostly fluid 样式主要由流体式栅格（fluid grid）构成。 无论是在大尺寸或者中等大小屏幕，它都能保持尺寸不变而仅仅只是调整边距以适应更宽的屏幕。在小屏幕上，流体式栅格布局会将主要内容重新排版，使栏目垂直堆栈排列。使用流体式栅格的一个最主要优点是通常只需要在大屏幕与小屏幕之间设置一个响应点即可。

[![gh](http://wf.uisdc.com/cn/layouts/rwd-patterns/imgs/mostly-fluid.svg)](view-source:wf.uisdc.com/cn/resources/samples/layouts/rwd-patterns/mostly-fluid.html)

在最小视图的情况下，每个内容 div 垂直堆栈排列。一旦屏幕的宽度达到600px时，主容器 div 保持 width: 100%，其余的次要 div如下图所示并排排列在主 div下方。如果屏幕宽度超过了800px，主容器 div 的宽度将固定并在屏幕上居中。

{% highlight css%}    
    .container {
      display: -webkit-flex;
      display: flex;
      -webkit-flex-flow: row wrap;
      flex-flow: row wrap;
    }

    .c1, .c2, .c3 {
      width: 100%;
    }

    @media (min-width: 600px) {
      .c1 {
        width: 60%;
        -webkit-order: 2;
        order: 2;
      }

      .c2 {
        width: 40%;
        -webkit-order: 1;
        order: 1;
      }

      .c3 {
        width: 100%;
        -webkit-order: 3;
        order: 3;
      }
    }


    @media (min-width: 800px) {
      .c2 {
        width: 20%;
      }

      .c3 {
        width: 20%;
      }
    }
{% endhighlight %}

###活动布局模型

Layout shifter布局是响应能力最强的布局样式，它通过多个响应点来适应多种屏幕宽度。这种布局的关键在于，并不是重新排列内容或者垂直排列列而是将其四处移动。由于每个响应点对应的布局相互之间有巨大的差异，所以保持内容一致的操作更加复杂并可能涉及改动元素内部内容而不是仅仅改变全局布局。

[![gh2](http://wf.uisdc.com/cn/layouts/rwd-patterns/imgs/layout-shifter.svg)](view-source:wf.uisdc.com/cn/resources/samples/layouts/rwd-patterns/layout-shifter.html)

这个简化了的示例展示了layout shifter的设计样式，在较小屏幕中的内容纵向垂直排列，但在较大的屏幕中，布局发生了很大的变化：左边是一个div而右边由两个垂直排列的div构成。
{% highlight css%}
    .container {
      display: -webkit-flex;
      display: flex;
      -webkit-flex-flow: row wrap;
      flex-flow: row wrap;
    }

    .c1, .c2, .c3, .c4 {
      width: 100%;
    }

    @media (min-width: 600px) {
      .c1 {
        width: 25%;
      }

      .c4 {
        width: 75%;
      }

    }

    @media (min-width: 800px) {
      .container {
        width: 800px;
        margin-left: auto;
        margin-right: auto;
      }
    }
{% endhighlight %}

###掉落列模型

对于全屏多栏目布局来说，column drop能够简单地在屏幕宽度变窄以致于容不下太多内容时自动纵向排列栏目，最终使每一个栏目都垂直堆栈排列。在这种布局样式下，响应点可以根据页面内容使用各种设计。


[![gh2](http://wf.uisdc.com/cn/layouts/rwd-patterns/imgs/column-drop.svg)](view-source:wf.uisdc.com/cn/resources/samples/layouts/rwd-patterns/column-drop.html)

与 mostly fluid 的示例一样, 在最小视图中纵向垂直排列内容，但在屏幕宽度超过600px后，主要与次要内容 div占据了屏幕的全部宽度。 Div的顺序被设定为根据CSS中的order属性进行排列。 屏幕宽度为800px时，三个内容 div全部一起出现并占据了全部屏幕宽度。

{% highlight css%}
 .container {
      display: -webkit-flex;
      display: flex;
      -webkit-flex-flow: row wrap;
      flex-flow: row wrap;
    }

    .c1, .c2, .c3 {
      width: 100%;
    }

    @media (min-width: 600px) {
      .c1 {
        width: 60%;
        -webkit-order: 2;
        order: 2;
      }

      .c2 {
        width: 40%;
        -webkit-order: 1;
        order: 1;
      }

      .c3 {
        width: 100%;
        -webkit-order: 3;
        order: 3;
      }
    }


    @media (min-width: 800px) {
      .c2 {
        width: 20%;
      }

      .c3 {
        width: 20%;
      }
    }
{% endhighlight %}    
 
 ----
 未完待续
