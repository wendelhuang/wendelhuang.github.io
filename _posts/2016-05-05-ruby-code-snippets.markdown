---
layout: post
title:  "My Ruby Code Snippets!"
date:   2016-05-05
categories: ruby
---

* 目录
{:toc}

***

# Ruby环境

## Ruby环境变量

### 修改Ruby的加载路径
{% highlight ruby %}
$:.unshift File.expand_path('..', __FILE__)
# 把当前路径加入到Ruby的LOAD_PATH中
# unshift是数组的一个方法，把指定的值加到数组的最前面
{% endhighlight %}
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

### 整形格式化输出
{% highlight ruby %}
## 1.输出长度为10，不够10个字符前面补空格
printf("%10d\n", 100)
## 2.输出长度为10，不够10个字符前面补0
printf("%010d\n", 100)
## 2.输出长度为10，不够10个字符前面补0，并且数字带正负号(此时正负号也占一位)
printf("%+010d\n", 100)
{% endhighlight %}

### 浮点型格式化输出
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

### 字符串格式化输出
{% highlight ruby %}
## 1.输出长度为10，不够10个字符前面补空格(右对齐)
printf("%10s\n", 'hello')
## 2.输出长度为10，不够10个字符后面补空格(左对齐)
printf("%-10s\n", 'hello')
{% endhighlight %}

# 目录和文件

## 目录和文件

### 遍历目录
{% highlight ruby %}
def get_file_list(path)  
  Dir.entries(path).each do |sub|  # 也可以用Dir.foreach(path) do |sub| 或者Dir[/tmp/*]
    if sub != '.' && sub != '..'  
      if File.directory?("#{path}/#{sub}")  
        puts "[#{sub}]"  
        get_file_list("#{path}/#{sub}")  
      else  
        puts "  |--#{sub}"  
      end  
    end  
  end  
end 
{% endhighlight %}

### 目录连接
{% highlight ruby %}
File.join('/', 'usr', 'bin')
#=>/usr/bin
{% endhighlight %}

### 文件名连接
{% highlight ruby %}
File.expand_path('../config/database.yml', "/tmp")
# => /config/database.yml
{% endhighlight %}

### 文件夹中文件列表
{% highlight ruby %}
# 列出根目录下所有目录及文件
Dir.glob('/*')
# 列出目录中所有yml文件
Dir.glob(File.join(RAILS_ROOT, 'config', 'locales', '*.yml'))
# 列出目录/usr /lib /sys
Dir.glob(File.join('/', '{usr,lib,sys}')) # 注意usr lib的逗号后面不要有空格
{% endhighlight %}

### 获取路径中文件名
{% highlight ruby %}
File.basename('/tmp/abc.log')
# 从路径名中移除目录，只保留文件名
# =>abc.log

File.basename('/tmp/abc.log', '.log')
# 从文件名中移除扩展名
# =>abc
# 或者
File.basename('/tmp/abc.log', '.*')
# =>abc
{% endhighlight %}

### 获取路径中目录
{% highlight ruby %}
File.dirname('/tmp/abc.log')
# 从路径名中移除文件名，只保留目录
# =>/tmp
{% endhighlight %}

### 当前路径名
{% highlight ruby %}
__FILE__
# 当前文件路径名
{% endhighlight %}
