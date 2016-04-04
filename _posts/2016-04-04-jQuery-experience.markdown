---
layout: post
title:  "My jQuery experience!"
date:   2016-04-04
categories: frontend javascript jQuery
---

* 目录
{:toc}

***

# 选择器

## 通过id选择

### 通过id选择
{% highlight ruby %}
$("#id")
#通过id选择页面元素
{% endhighlight %}

### 通过class选择
{% highlight ruby %}
$(".id")
#通过class选择页面元素
{% endhighlight %}

### 通过name选择
{% highlight ruby %}
$("input[name='xxx']")
#选择所有的name属性等于'xxx'的input元素 

$("input[name!='xxx']") 
#选择所有的name属性不等于'xxx'的input元素 

$("input[name^='xxx']")
#选择所有的name属性以'xxx'开头的input元素 

$("input[name$='xxx']")
#选择所有的name属性以'xxx'结尾的input元素 

$("input[name*='xxx']")
#选择所有的name属性包含'xxx'的input元素 
{% endhighlight %}

# 设置元素的值

## 设置元素的值

### 通过val()设置元素的值
{% highlight ruby %}
$(".sex").val(1);
#设置class为sex的元素的value=1
{% endhighlight %}

