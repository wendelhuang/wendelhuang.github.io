---
layout: post
title:  "My Ruby Code Snippets!"
date:   2016-05-05
categories: ruby
---

* 目录
{:toc}

***

# 输入输出

## 格式化输出

### 格式化输出
{% highlight ruby %}
#格式化输出的方法
puts "%d" % 100
#或者
printf("%d\n", 100)
#或者
puts format("%d\n", 100)
{% endhighlight %}

整形格式化输出
{% highlight ruby %}
## 1.输出长度为10，不够10个字符前面补空格
printf("%10d\n", 100)
## 2.输出长度为10，不够10个字符前面补0
printf("%010d\n", 100)
## 2.输出长度为10，不够10个字符前面补0，并且数字带正负号(此时正负号也占一位)
printf("%+010d\n", 100)
{% endhighlight %}

浮点型格式化输出
{% highlight ruby %}
## 1.小数点保留2位小数
printf("%.2f\n", 1.11111)
## 2.输出长度为10，小数点保留2位小数，不够10个字符前面补空格
printf("%10.2f\n", 1.11111)
## 3.输出长度为10，小数点保留2位小数，不够10个字符前面补0
printf("%010.2f\n", 1.11111)
## 4.输出长度为10，小数点保留2位小数，不够10个字符前面补0，并且数字带正负号(此时正负号也占一位)
printf("%+010.2f\n", 1.11111)
{% endhighlight %}

字符串格式化输出
{% highlight ruby %}
## 1.输出长度为10，不够10个字符前面补空格(右对齐)
printf("%10s\n", 'hello')
## 2.输出长度为10，不够10个字符后面补空格(左对齐)
printf("%-10s\n", 'hello')
{% endhighlight %}
