---
layout: post
title: CSS清除浮动几种方法的总结
date: 2016-07-04 19:30:00
type: CSS
comment: y
---

>清除浮动是每一个 web前台设计师必须掌握的机能。css清除浮动大全，共8种方法。 

浮动会使当前标签产生向上浮的效果，同时会影响到前后标签、父级标签的位置及 width height 属性。而且同样的代码，在各种浏览器中显示效果也有可能不相同，这样让清除浮动更难了。解决浮动引起的问题有多种方法，但有些方法在浏览器兼容性方面还有问题。 

下面总结8种清除浮动的方法（测试已通过 ie chrome firefox opera，后面三种方法只做了解就可以了）： 





###1，父级div定义 height 


{% highlight javascript %}
    <style type="text/css"> 
    .div1{background:#000080;border:1px solid red;/*解决代码*/height:200px;} 
    .div2{background:#800080;border:1px solid red;height:100px;margin-top:10px} 
    .left{float:left;width:20%;height:200px;background:#DDD} 
    .right{float:right;width:30%;height:80px;background:#DDD} 
    </style> 
    <div class="div1"> 
    <div class="left">Left</div> 
    <div class="right">Right</div> 
    </div> 
    <div class="div2"> 
    div2 
    </div> 
{% endhighlight %}



原理：父级div手动定义height，就解决了父级div无法自动获取到高度的问题。 

优点：简单、代码少、容易掌握 

缺点：只适合高度固定的布局，要给出精确的高度，如果高度和父级div不一样时，会产生问题 

建议：不推荐使用，只建议高度固定的布局时使用 

###2，结尾处加空div标签 clear:both 

{% highlight javascript %}
    <style type="text/css"> 
    .div1{background:#000080;border:1px solid red} 
    .div2{background:#800080;border:1px solid red;height:100px;margin-top:10px} 
    .left{float:left;width:20%;height:200px;background:#DDD} 
    .right{float:right;width:30%;height:80px;background:#DDD} 
    /*清除浮动代码*/ 
    .clearfloat{clear:both} 
    </style> 
    <div class="div1"> 
    <div class="left">Left</div> 
    <div class="right">Right</div> 
    <div class="clearfloat"></div> 
    </div> 
    <div class="div2"> 
    div2 
    </div> 
{% endhighlight %}

原理：添加一个空div，利用css提高的clear:both清除浮动，让父级div能自动获取到高度 

优点：简单、代码少、浏览器支持好、不容易出现怪问题 

缺点：不少初学者不理解原理；如果页面浮动布局多，就要增加很多空div，让人感觉很不好 

建议：不推荐使用，但此方法是以前主要使用的一种清除浮动方法 

###3，父级div定义 伪类:after 和 zoom 

{% highlight javascript %}
	<style type="text/css"> 
	.div1{background:#000080;border:1px solid red;} 
	.div2{background:#800080;border:1px solid red;height:100px;margin-top:10px} 
	.left{float:left;width:20%;height:200px;background:#DDD} 
	.right{float:right;width:30%;height:80px;background:#DDD} 
	/*清除浮动代码*/ 
	.clearfloat:after{display:block;clear:both;content:"";visibility:hidden;height:0} 
	.clearfloat{zoom:1} 
	</style> 
	<div class="div1 clearfloat"> 
	<div class="left">Left</div> 
	<div class="right">Right</div> 
	</div> 
	<div class="div2"> 
	div2 
	</div> 
{% endhighlight %}
原理：IE8以上和非IE浏览器才支持:after，原理和方法2有点类似，zoom(IE转有属性)可解决ie6,ie7浮动问题 

优点：浏览器支持好、不容易出现怪问题（目前：大型网站都有使用，如：腾迅，网易，新浪等等） 

缺点：代码多、不少初学者不理解原理，要两句代码结合使用才能让主流浏览器都支持。 

建议：推荐使用，建议定义公共类，以减少CSS代码。 

###4，父级div定义 overflow:hidden 

{% highlight javascript %}
	<style type="text/css"> 
	.div1{background:#000080;border:1px solid red;/*解决代码*/width:98%;overflow:hidden} 
	.div2{background:#800080;border:1px solid red;height:100px;margin-top:10px;width:98%} 
	.left{float:left;width:20%;height:200px;background:#DDD} 
	.right{float:right;width:30%;height:80px;background:#DDD} 
	</style> 
	<div class="div1"> 
	<div class="left">Left</div> 
	<div class="right">Right</div> 
	</div> 
	<div class="div2"> 
	div2 
	</div> 
{% endhighlight %}

原理：必须定义width或zoom:1，同时不能定义height，使用overflow:hidden时，浏览器会自动检查浮动区域的高度 

优点：简单、代码少、浏览器支持好 

缺点：不能和position配合使用，因为超出的尺寸的会被隐藏。 

建议：只推荐没有使用position或对overflow:hidden理解比较深的朋友使用。 

###5，父级div定义 overflow:auto 

{% highlight javascript %}
	<style type="text/css"> 
	.div1{background:#000080;border:1px solid red;/*解决代码*/width:98%;overflow:auto} 
	.div2{background:#800080;border:1px solid red;height:100px;margin-top:10px;width:98%} 
	.left{float:left;width:20%;height:200px;background:#DDD} 
	.right{float:right;width:30%;height:80px;background:#DDD} 
	</style> 
	<div class="div1"> 
	<div class="left">Left</div> 
	<div class="right">Right</div> 
	</div> 
	<div class="div2"> 
	div2 
	</div> 
{% endhighlight %}

原理：必须定义width或zoom:1，同时不能定义height，使用overflow:auto时，浏览器会自动检查浮动区域的高度 

优点：简单、代码少、浏览器支持好 

缺点：内部宽高超过父级div时，会出现滚动条。 

建议：不推荐使用，如果你需要出现滚动条或者确保你的代码不会出现滚动条就使用吧。 

###6，父级div 也一起浮动 

{% highlight javascript %}
	<style type="text/css"> 
	.div1{background:#000080;border:1px solid red;/*解决代码*/width:98%;margin-bottom:10px;float:left} 
	.div2{background:#800080;border:1px solid red;height:100px;width:98%;/*解决代码*/clear:both} 
	.left{float:left;width:20%;height:200px;background:#DDD} 
	.right{float:right;width:30%;height:80px;background:#DDD} 
	</style> 
	<div class="div1"> 
	<div class="left">Left</div> 
	<div class="right">Right</div> 
	</div> 
	<div class="div2"> 
	div2 
	</div> 
{% endhighlight %}

原理：所有代码一起浮动，就变成了一个整体 

优点：没有优点 

缺点：会产生新的浮动问题。 

建议：不推荐使用，只作了解。 

###7，父级div定义 display:table 

{% highlight javascript %}
	<style type="text/css"> 
	.div1{background:#000080;border:1px solid red;/*解决代码*/width:98%;display:table;margin-bottom:10px;} 
	.div2{background:#800080;border:1px solid red;height:100px;width:98%;} 
	.left{float:left;width:20%;height:200px;background:#DDD} 
	.right{float:right;width:30%;height:80px;background:#DDD} 
	</style> 
	<div class="div1"> 
	<div class="left">Left</div> 
	<div class="right">Right</div> 
	</div> 
	<div class="div2"> 
	div2 
</div> 
{% endhighlight %}
原理：将div属性变成表格 

优点：没有优点 

缺点：会产生新的未知问题。 

建议：不推荐使用，只作了解。 

###8，结尾处加 br标签 clear:both 

{% highlight javascript %}
	<style type="text/css"> 
	.div1{background:#000080;border:1px solid red;margin-bottom:10px;zoom:1} 
	.div2{background:#800080;border:1px solid red;height:100px} 
	.left{float:left;width:20%;height:200px;background:#DDD} 
	.right{float:right;width:30%;height:80px;background:#DDD} 
	.clearfloat{clear:both} 
	</style> 
	<div class="div1"> 
	<div class="left">Left</div> 
	<div class="right">Right</div> 
	<br class="clearfloat" /> 
	</div> 
	<div class="div2"> 
	div2 
	</div> 
{% endhighlight %}
原理：父级div定义zoom:1来解决IE浮动问题，结尾处加 br标签 clear:both 

建议：不推荐使用，只作了解。

---

另外新的 flexbox 布局模式被用来重新定义CSS中的布局方式，完全不用考虑清除浮动的事。很遗憾的是最近规范变动过多，导致各个浏览器对它的实现也有所不同。不过我仍旧想要分享一些例子，来让你知道即将发生的改变。这些例子目前只能在支持 flexbox 的 Chrome 浏览器中运行，基于最新的标准。<br>

网上有不少过时的 flexbox 资料。 如果你想要了解更多有关 flexbox 的内容，从这里学习如何辨别一份资料是否过时。这里是[一份关于最新标准的详细文章](https://bocoup.com/weblog/dive-into-flexbox)。

还有一个特别萌的[CSS布局网站](http://zh.learnlayout.com/)，保证都能看懂的。