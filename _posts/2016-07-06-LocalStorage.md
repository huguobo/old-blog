---
layout: post
title: sessionStorage、localStorage如何存储数组与对象
date: 2016-07-06 09:45:00
type: H5
comment: y
---


> sessionStorage和localStorage做为HTML5新特性，被广泛应用于客户端缓存技术。不过这个有个误区，两者虽然对存储的内容大小没有限制，但是存入的东西都被转换成了字符串，也就是说无法存入数组或者对象，就算存入了也会被转化为字符串。不过实际开发过程中 缓存的数据一般都是 数组或者json对象，那么应该怎么处理呢？


##1.存数组

{% highlight javascript %}
    //先举个例子(以sessionStorage为例)
    var aa=[1,2,3];
    var sStorage=window.sessionStorage;
    sStorage.aa=aa;
    console.log(sStorage.aa); //输出1,2,3

    /*下面我写个函数*/
    function stringToArray(arr){
        return arr.split(','); /*好吧，这个比较喽 @_@ */
    }

    /*稍微优化一下*/
    function stringToArray(arr){
        var tempArr=arr.split(',');
        var returnArr=new Array();
        var i,len=tempArr.length;
        for(i=0;i<len;i++){
            if(typeOf(tempArr[0]*1)==='number'){
                returnArr.push(tempArray[i]*1);
            }else{
                returnArr.push(tempArray[i]);
            }
        }
        return returnArr;
    }

    /*其实还有很多复杂的情况，我这里就不一一写了，实际开发中要注意变量类型*/
{% endhighlight %}
---

##2存Json对象
{% highlight javascript %}
    /*思路很简单：JSON对象提供的parse和stringify将其他数据类型转化成字符串，再存储到storage中就可以了*/
    var obj = { Hellow:'world' }; 
    var str = JSON.stringify(obj); 

    //存入 
    sessionStorage.obj = str; 
    //读取 
    str = sessionStorage.obj; 
    //重新转换为对象 
    obj = JSON.parse(str)
{% endhighlight %}

---
最近在做Healthy Chart，一款给我女朋友做的记录健康情况的本地web应用，其实用C#和数据库特别好完成，但是想试试用WEB做。发现JS读写本地文件限制太大，而且NodeJs写个服务器，又没必要，又不想弄数据库，就想到了**LocalStorage**，实现ing，希望可以完成~~