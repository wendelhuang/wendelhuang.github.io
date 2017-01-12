---
layout: post
title:  "My Interview Summary"
date:   2017-01-12
categories: interview
---

* 目录
{:toc}

***

# jQuery

## 跳出each循环方法
{% highlight js %}
return true;//相当于continue
return false;//相当于break
$("div[class='xxx']").each(
  function(index){
    if(index<1){
      console.log(index + " executed");
    }else{
      console.log(index + " continue");
      return true;
      //console.log(index + " break");
      //return false;
    }
  }
);
{% endhighlight %}

## 获取id=a的p标签下的所有class=a的超链接
{% highlight js %}
$("p[id='a']>a[class='a']").each(
  function(index) {
    console.log($(this).attr("href"));
  }
);
{% endhighlight %}

# java

## HashMap和Hashtable的区别
