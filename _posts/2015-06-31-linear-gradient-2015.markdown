---
layout:     post
header-img: "img/post-bg-universe.jpg"
title:      "背景渐变"
subtitle:   "css背景半透明渐变"
date:       2015-06-31 12:00:00
author:     "LiBei"
tags:
    - 前端技术
    - css
---

> “Linear-gradient”

首先针对各个浏览器的内核不同，实现的方法不同，

{% highlight css %}
 background: -webkit-linear-gradient(top,rgba(255, 255, 255, .5) 25%,rgba(255, 255, 255, 0) 100%);
 background: -moz-linear-gradient(top,rgba(255, 255, 255, .5) 25%, rgba(255, 255, 255, 0) 100%);
{% endhighlight %}

然而IE8以下是不支持rgba的，因此对使用了滤镜

{% highlight css %}
filter:alpha(opacity=50 finishopacity=0 style=1 startx=0,starty=25,finishx=0,finishy=100);
{% endhighlight %}
写完滤镜后，发现IE6-9有效，IE10无效，于是
{% highlight css %}
background: -ms-linear-gradient(top,rgba(255, 255, 255, .5) 25%, rgba(255, 255, 255, 0) 100%);
{% endhighlight %}

终于背景的透明出现了，然而！IE89的字体却不再出现了。。。。 后来发现，子元素继承了父元素的透明属性，所以，把父元素的position设置为static，子元素position设置为relative，终于!全都出现字体了！！！！ 但是，原来父级靠absolute控制位置，始终位于祖父元素的底部，文字增多的情况下，就像上增长，底部始终不变的。 现在，就控制不了了。。文字一多，就向下生长了。。。哭。。这个问题还米有解决。
PS，页面扔然很多问题，比如:border-radius没有实现IE8，比如刚刚的例子并没有实现渐变2次。。加油！


—— Libei 后记于 2016.10
