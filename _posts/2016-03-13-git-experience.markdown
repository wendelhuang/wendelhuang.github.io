---
layout: post
title:  "My git experience!"
date:   2016-03-12
categories: tools git
---

* 目录
{:toc}

***

# 分支

## 查看分支

### 列出本地分支
{% highlight ruby %}
git branch
{% endhighlight %}

### 列出本地及远程分支
{% highlight ruby %}
git branch -a
{% endhighlight %}

## 创建分支

### 创建分支
{% highlight ruby %}
git branch BRANCHNAME
{% endhighlight %}

### 切换分支
{% highlight ruby %}
git checkout BRANCHNAME
# 切换到已经创建好的分支
git checkout -b BRANCHNAME
# 创建分支并切换到该新建分支
{% endhighlight %}

## 删除分支

### 删除本地分支
{% highlight ruby %}
git branch -D BRANCHNAME
{% endhighlight %}

### 删除远程分支
{% highlight ruby %}
git push origin :BRANCHNAME
# 注意冒号:
{% endhighlight %}

## 合并分支

### 合并分支
{% highlight ruby %}
git push origin master
# 切换到master分支
git merge BRANCHNAME
# 合并分支到master分支
git commit
{% endhighlight %}

