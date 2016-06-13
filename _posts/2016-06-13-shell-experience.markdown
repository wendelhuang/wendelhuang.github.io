---
layout: post
title:  "My Shell experience"
date:   2016-06-13
categories: shell
---

* 目录
{:toc}

***

# 文本处理

## 替换文件夹下所有文本
{% highlight bash %}
ls -l * | awk '{print "sed 's/被替换的内容/要替换的内容/g' "$1" >temp/"$1}' > sed.sh
{% endhighlight %}
生成的脚本内容如下所示
{% highlight bash %}
sed s/aaaaaa/bbb/g a.txt > temp/a.txt
sed s/aaaaaa/bbb/g b.txt > temp/b.txt
sed s/aaaaaa/bbb/g c.txt > temp/c.txt
sed s/aaaaaa/bbb/g d.txt > temp/d.txt
{% endhighlight %}
执行脚本即可

## 分割字符串
使用cut分割，简洁方便，但是只支持单个字符分割，比如文本a.txt内容为
{% highlight bash %}
10.221.1.1 1
10.221.1.1 2
10.221.1.3 15
{% endhighlight %}
执行
{% highlight bash %}
cat a.txt | cut -d ' ' -f1
{% endhighlight %}
结果为
{% highlight bash %}
10.221.1.1
10.221.1.1
10.221.1.3
{% endhighlight %}
  
使用awk处理如下
{% highlight bash %}
cat a.txt | awk -F ' ' '{print $1}'
{% endhighlight %}
效果一样，而且awk可以支持多个字符作分割符

## 从字符串中删除指定字符
{% highlight bash %}
echo 'aaabbccb' | tr -d 'bb'
# aaaccb
{% endhighlight %}

