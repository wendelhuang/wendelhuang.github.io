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
{% highlight javascript %}
$("#id")
#通过id选择页面元素
{% endhighlight %}

### 通过class选择
{% highlight javascript %}
$(".id")
#通过class选择页面元素

#选择具有多个class的元素,比如<div class="modal fade in"></div>
$(".modal.fade").filter("in")

$("[class='modal fade in']")
#此处顺序必须一致才行

$(".modal.fade.in") 
{% endhighlight %}

### 通过name选择
{% highlight javascript %}
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

# 页面元素操作

## 设置元素的值

### 通过val()设置元素的值
{% highlight javascript %}
$(".sex").val(1);
#设置class为sex的元素的value=1
{% endhighlight %}

## 设置元素的class

### 通过removeClass()和addClass()设置元素的class
{% highlight javascript %}
$(".btn.active").removeClass('active');
#删除class为btn active的元素其中的active
#如果删除多个class,中间以空格分开
#如果不加参数,移除所有class
$(".btn").addClass('active');
#为class为btn的元素添加class active
{% endhighlight %}

## form相关

### 提交form
{% highlight javascript %}
$("#id_of_form").submit();
{% endhighlight %}

