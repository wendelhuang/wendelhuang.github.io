---
layout: post
title:  "My git experience!"
date:   2016-03-12
categories: tools git
---

* 目录
{:toc}

***

# 配置

git的配置项有3个层级，分别是仓库级(git config --local)，全局级(git config --global)以及系统级(git config --system)。  
优先级仓库级>全局级>系统级  
仓库级的配置文件是repository下的.git/config文件，只对当前repository有效  
全局级的配置文件是用户home目录下的.gitconfig文件，对系统中本用户有效  
系统级的配置文件是/etc/gitconfig文件，对当前系统所有用户有效  

文件内容示例如下
{% highlight bash %}
[core]
  repositoryformatversion = 0
  filemode = true
  bare = false
  logallrefupdates = true
[remote "origin"]
  url = git@github.com:xxxxxx/xxxxxx.github.io.git
  fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
  remote = origin
  merge = refs/heads/master
[user]
  name = xxxxxxxx
  email = xxxxxxxx@example.com
{% endhighlight %}

## 配置查看
{% highlight bash %}
git config --global -l
{% endhighlight %}

## 配置项示例

### 配置用户名邮箱
{% highlight bash %}
git config --global user.name "username"
git config --global user.email "username@example.com"
{% endhighlight %}

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

