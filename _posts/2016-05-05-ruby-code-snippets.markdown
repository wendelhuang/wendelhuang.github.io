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

# 表达式

## 表达式

### == and equal? and ===
equal?用来比较两个对象是否是同一个引用,比如：
{% highlight ruby %}
a = "Ruby"       # 一个字符串对象。
b = c = "Ruby"   # 两个字符串对象指向动一个引用。
a.equal?(b)      # false: a和b是不同的对象。
b.equal?(c)      # true: b和c指向同一个引用。
#这种比较方式实际上是比较两个对象的ID是否相同，显然a是一个对象，而b和c指向另一个对象，他们的对象ID是不同的：
a.object_id == b.object_id   # 等同于 a.equal?(b)
{% endhighlight %}
  
==用来比较两个对象的值是不是一样
数组和哈希也定义了==操作符，如果两个数组或两个哈希对象中元素个数相同，且每个元素都相同，那么==返回true.
需要注意的是,Numerics对象在比较的时候会做一个简单的最新转换，所以Fixnum类型的1和Float类型的1.0的比较结果是相等。
{% highlight ruby %}
1 == 1.0 # true
{% endhighlight %}
  
eql?也是比较两个对象的值，如果重新定义了子类的 == 方法，一般需要 alias 到 eql? 方法。和==不同的是
{% highlight ruby %}
1.eql?(1.0) # false
{% endhighlight %}
eql?用来哈希中key值的比较
{% highlight ruby %}
pry(main)> hash = Hash.new
#=> {}
pry(main)> hash[2] = "a"
#=> "a"
pry(main)> hash[2.0] = "b"
#=> "b"
pry(main)> hash[2]
#=> "a"
pry(main)> hash[2.0]
#=> "b"
pry(main)> hash[2.00] = "c"
#=> "c"
pry(main)> hash[2.0]
#=> "c"
{% endhighlight %}
  
===通常用在 case 比较调用该方法，比如
{% highlight ruby %}
case some_object
when /a regex/
 # The regex matches
when String
 # some_object is kind of String
when 2..4
 # some_object is in the range 2..4
when lambda {|x| some_crazy_custom_predicate }
 # the lambda returned true
end
{% endhighlight %}
等同于
{% highlight ruby %}
if /a regex/ === some_object
 # The regex matches
elsif String === some_object
 # some_object is kind of object
elsif (2..4) === some_object
 # some_object is in the range 2..4
elsif lambda {|x| some_crazy_custom_predicate } === some_object
 # the lambda returned true
end
{% endhighlight %}

### 多个变量同时赋值
{% highlight ruby %}
a, b = 1, 2
# a=1
# b=2
(a, b, c) = [1, 2, 3]
# a=1
# b=2
# c=3
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
