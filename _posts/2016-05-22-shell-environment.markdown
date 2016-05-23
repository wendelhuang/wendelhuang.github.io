---
layout: post
title:  "小技巧: 因为shell环境造成的ssh客户端tab键，方向键，backspace，delete都不正常输入"
date:   2016-05-22
categories: tools linux shell
---

使用aliyun的ECS的时候我遇到了一个"棘手"的问题，在windows下使用ssh客户端连上去后tab键，方向键，backspace，delete键都不能正常使用  
查了许久发现是使用的shell环境的问题  
默认登录服务器后使用
{% highlight bash %}
echo $0
#=> -sh
{% endhighlight %}
发现默认的shell环境是bsh  
执行
{% highlight bash %}
/bin/bash
{% endhighlight %}
切换到bash一切就正常了
