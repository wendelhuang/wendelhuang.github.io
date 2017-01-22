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

## java基础

### HashMap和Hashtable的区别

### 运行时异常和非运行时异常的区别并举例

# 框架

## spring

### 使用自定义annotation实现日志功能

# 算法

## 数论

### String类型的变量s1和s2都是数字组成的字符串，实现s1*s2

### 编号为1-100的100个人，房间里有编号为1-100的100个灯泡，初始都为不亮的状态，从编号为1的人开始进入房间每个人都将自己编号倍数编号的灯泡改变状态，问最后哪些灯泡是亮着的

### 将数字n进行质数分解

## 数据结构

### 单链表反转

## 递归和分治

### 一个数组是先增后减的数组，求数组最大值的下标



# 数据库

# 网络

## HTTP和HTTPS的关系

## HTTP协议状态编码

## TCP协议建立连接的过程，在建立连接过程中客户端和服务器的端口状态

# 系统设计

## 设计模式

### java类库用到的3种不同的设计模式，列出java类和使用的设计模式

# linux
