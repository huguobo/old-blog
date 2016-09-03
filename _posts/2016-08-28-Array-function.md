---
layout: post
title:    对Map，foreach，reduce和filter的理解
date: 2016-08-28 19:25:00
type: Javascript Array
comment: y
---

>学习过程中关于Array对象的几个内置函数一直有些疑问,对于`Map`，`foreach`,`reduce`和`filter`的区别一直混淆不清~，通过查阅资料，形象化的描述一下他们的区别，在这里记录一下：

### ForEach
假设我们有一个数组，每个元素是一个人。你面前站了一排人。

foreach 就是你按顺序一个一个跟他们做点什么，具体做什么，随便:

{% highlight javascript %}
people.forEach(function (dude) {
  dude.pickUpSoap();
});
{% endhighlight %}





### Map

map 就是你手里拿一个盒子（一个新的数组），一个一个叫他们把钱包扔进去。结束的时候你获得了一个新的数组，里面是大家的钱包，钱包的顺序和人的顺序一一对应。

{% highlight javascript %}
var wallets = people.map(function (dude) {
  return dude.wallet;
});
{% endhighlight %}

### Reduce

reduce 就是你拿着钱包，一个一个数过去看里面有多少钱啊？每检查一个，你就和前面的总和加一起来。这样结束的时候你就知道大家总共有多少钱了。


{% highlight javascript %}
var totalMoney = wallets.reduce(function (countedMoney, wallet) {
  return countedMoney + wallet.money;
}, 0);
{% endhighlight %}

###Filter

你一个个钱包数过去的时候，里面钱少于 100 块的不要（留在原来的盒子里），多于 100 

块的丢到一个新的盒子里。这样结束的时候你又有了一个新的数组，里面是所有钱多于 100 块的钱包：

{% highlight javascript %}
var fatWallets = wallets.filter(function (wallet) {
  return wallet.money > 100;
});
{% endhighlight %}

最后要说明一点这个类比和实际代码的一个区别，那就是 map 和 filter 都是 immutable 
methods，也就是说它们只会返回一个新数组，而不会改变原来的那个数组，所以这里 filter 的例子是和代码有些出入的（原来的盒子里的钱包减少了），但为了形象说明，大家理解就好

最后附上一张数组迭代方法的图：

![](http://pic2.zhimg.com/08235a5dafaaba6f9418704cba12fedd_b.jpeg)

