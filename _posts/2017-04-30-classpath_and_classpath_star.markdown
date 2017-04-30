---
layout: post
title:  "classpath vs classpath*"
date:   2017-04-30
categories: java spring
---

* 目录
{:toc}

jUnit Test遇到org.apache.ibatis.binding.BindingException
在运行jUnit Test的时候遇到了一个异常情况
![](/images/2017-04-30-classpath/1.png)
直觉观察可以得出，运行jUnit Test时没有找到对应的MyBatis XML文件来解析。

可是为什么系统运行正常，但是使用jUnit Test就正常呢？  带着疑问查看了一下console输出的日志信息，发现有一点不太正常的地方。
![](/images/2017-04-30-classpath/2.png)
注意红框中的信息，在上一个红框中，扫描XML文件是在classes目录中进行，下一个扫描XML文件却是在test-classes目录中扫描(因为在maven创建的test用例和main代码文件夹同级)，结果扫描到的XML为空（红框所示）。很明显是因为test-classes文件夹覆盖了classes文件夹，而且扫描完test-classes目录后扫描终止，并没有继续去扫描classes文件夹了。

因此联系到配置文件中classpath和classpath*的区别，很快找到了问题所在。
![](/images/2017-04-30-classpath/3.png)
因为这里是classpath导致，扫描终止，将classpath改为classpath*即可解决这一问题。
