---
layout: post
title:  "My Rails experience!"
date:   2016-04-09
categories: rails
---

* 目录
{:toc}

***

# Assets

## 配置

### assets查找路径
{% highlight ruby %}
#assets的路径在
Rails.application.config.assets.paths
{% endhighlight %}

### 修改assets查找路径
在config/application.rb中添加
{% highlight ruby %}
config.assets.paths += %w{js css img}.map{|dir| Rails.root.join("parent_dir", dir) }
{% endhighlight %}

Rails4中可以在config/initializers/assets.rb中添加
{% highlight ruby %}
Rails.application.config.assets.paths << Rails.root.join("parent_dir", "dir")
{% endhighlight %}

### vendor目录
1. vendor目录下的子目录，默认自动被加入assets查找路径
