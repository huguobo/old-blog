---
layout: post
title: css3中关于transform，transiton和animate的理解
date: 2016-11-15 22:00:00
type: css3
comment: y
---

>CSS3中关于Transform，Transtion和Animate的理解

###1.Transform

**transform 是实现的是元素的变形（静态）**

主要使用有

- transform：translate() 平移 
- transform：rotate() 旋转 
- transform-origin: x, y 主要结合rotate来使用 规定旋转的中心点再哪 
- transform：scale() 缩放 
- transform：skew() 倾斜

---





###2. Transition

**transition是实现的是动画的过程**

主要使用有

- transition: all .5s ease-in-out 1s; 
- transition-property ：all | none | indent 属性改变时执行transition效果 
- transition-duration ：动画所需的时间 
- transition-timing-function 改变属性值的变换速率 
- transition-delay 动画延迟多久才开始

---
###3. Animation

**animation是transition的一个拓展**

- animation中增加了一个keyframes属性来定义动画的时间轴和关键帧 
- animation-name 绑定到选择器的 keyframe 名称 
- animation-duration 成动画所花费的时间 
- animation-timing-function 规定动画的速度曲线 
- animation-delay 规定在动画开始之前的延迟。 
- animation-iteration-count 规定动画应该播放的次数 
- animation-direction 规定是否应该轮流反向播放动画


{% highlight css%}
  @keyframes mykeyframes{
    0%{

    }
     50%{
     }
     100%{
     }
   }
{% endhighlight %}

---