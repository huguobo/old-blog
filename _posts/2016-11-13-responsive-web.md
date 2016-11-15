---
layout: post
title: 多设备布局:响应式设计模型二
date: 2016-11-13 22:00:00
type: Responsive-Web-Design-Patterns
comment: y
---


>虽然响应式网页设计样式正在快速发展，但能够完全兼容桌面级设备与移动设备的成熟样式却是屈指可数。



###设计模型

为了创建简洁易懂的示例，下面提到的每一个案例都是基于flexbox通过真实的标签创建的, 主要是在一个主 div内包含三个内容 div。 每个示例都由定义最小视图开始，并在必要的时候加入响应节点（breakpoint）。 flexbox 布局模式 能很好的支持现在的主流浏览，尽管为了最佳效果你可能需要依赖特定的前缀。

###微调模型

Tiny tweaks会对布局做出细微的改动，如调整字体大小，缩放图片尺寸或者微调内容位置等等。这种布局样式对于单列排版来说十分合适，比如一些单页面的长网站和含有大量文字内容的页面。

顾名思义，这个示例的变化随着屏幕大小的变化而改变。当屏幕宽度越大，字体大小和内边距值也会随之变大。

[![gh](http://wf.uisdc.com/cn/layouts/rwd-patterns/imgs/tiny-tweaks.svg)](http://wf.uisdc.com/cn/resources/samples/layouts/rwd-patterns/tiny-tweaks.html)

{% highlight css%}
     .c1 {
      padding: 10px;
      width: 100%;
     }

    @media (min-width: 500px) {
      .c1 {
        padding: 20px;
        font-size: 1.5em;
      }
    }

    @media (min-width: 800px) {
      .c1 {
        padding: 40px;
        font-size: 2em;
      }
    }
    
{% endhighlight %}
 
 
###画布溢出布局

不采用垂直堆叠内容的方式，画布溢出模式减少经常使用的内容，或许使导航或应用菜单超出屏幕，只 当屏幕上显示的大小足够时才显示它们，并在较小的屏幕将内容变成一个点击。

[![](http://wf.uisdc.com/cn/layouts/rwd-patterns/imgs/off-canvas.svg)](http://wf.uisdc.com/cn/resources/samples/layouts/rwd-patterns/off-canvas.html)

不采用垂直堆叠内容的方式，这个示例使用一种transform: translate(-250px, 0)的变换隐藏了超出内容的两个div。JavaScript通过对元素添加一个开放的类来显示div。屏幕更宽，溢出屏幕定位则移除元素并使得 他们在可见的视图显示。
使用该示例时注意, iOS 6的Safari浏览器以及安卓浏览器不支持flexbox的flex-flow: row nowrap特性,所以我们必须回到绝对定位的方式

{% highlight css %}
    body {
      overflow-x: hidden;
    }
    
    .container {
      display: block;
    }

    .c1, .c3 {
      position: absolute;
      width: 250px;
      height: 100%;
    
      /*
        This is a trick to improve performance on newer versions of Chrome
        #perfmatters
      */
      -webkit-backface-visibility: hidden;
      backface-visibility: hidden;

      -webkit-transition: -webkit-transform 0.4s ease-out;
      transition: transform 0.4s ease-out;
    
      z-index: 1;
    }

    .c1 {
      /*
      Using translate3d as a trick to improve performance on older versions of Chrome
      See: http://aerotwist.com/blog/on-translate3d-and-layer-creation-hacks/
      #perfmatters
      */
      -webkit-transform: translate(-250px,0);
      transform: translate(-250px,0);
    }

    .c2 {
      width: 100%;
      position: absolute;
    }
    
    .c3 {
      left: 100%;
    }

    .c1.open {
      -webkit-transform: translate(0,0);
      transform: translate(0,0);
    }

    .c3.open {
      -webkit-transform: translate(-250px,0);
      transform: translate(-250px,0);
    }
    
    @media (min-width: 500px) {
      /* If the screen is wider then 500px, use Flexbox */
      .container {
        display: -webkit-flex;
        display: flex;
        -webkit-flex-flow: row nowrap;
        flex-flow: row nowrap;
      }
      .c1 {
        position: relative;
        -webkit-transition: none 0s ease-out;
        transition: none 0s ease-out;
        -webkit-transform: translate(0,0);
        transform: translate(0,0);
      }
      .c2 {
        position: static;
      }
    }

    @media (min-width: 800px) {
      body {
        overflow-x: auto;
      }
      .c3 {
        position: relative;
        left: auto;
        -webkit-transition: none 0s ease-out;
        transition: none 0s ease-out;
        -webkit-transform: translate(0,0);
        transform: translate(0,0);
      }
    }
    
{% endhighlight %}