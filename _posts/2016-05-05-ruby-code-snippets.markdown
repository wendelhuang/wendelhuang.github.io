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

### split
{% highlight ruby %}
a, b = "aa|bb|cc".split("|")
# a: 'aa'
# b: 'bb'
{% endhighlight %}

## 数组元素基本操作

### 追加元素到数组末尾
{% highlight ruby %}
# method 1
a = [1,2,3,4,5]＃=> [1,2,3,4,5] 
a << 99＃=> [1,2,3,4,5,99] 

# method 2
a = [1,2,3,4,5] 
a.push（10）＃=> [1，2，3，4，5，10]
{% endhighlight %}
  
### 追加元素到数组开头
{% highlight ruby %}
a = [1,2,3,4,5]＃=> [1,2,3,4,5] 
a.unshift(99) ＃=> [99,1,2,3,4,5]
{% endhighlight %}
  
### 从数组末尾弹出元素
{% highlight ruby %}
a = [1,2,3,4,5]＃=> [1,2,3,4,5] 
a.pop ＃=> [1,2,3,4]
{% endhighlight %}
  
### 从数组开头弹出元素
{% highlight ruby %}
a = [1,2,3,4,5]＃=> [1,2,3,4,5] 
a.shift ＃=> [2,3,4,5]
{% endhighlight %}

### 截取子数组
{% highlight ruby %}
a = [1,2,3,4,5]

p a[0,2] #=> [1, 2]
p a[1..3] #=> [2, 3, 4]
p a.slice(0,2) #=> [1, 2]
p a.slice(1..3) #=> [2, 3, 4]
{% endhighlight %}

### 数组填充
{% highlight ruby %}
a = [1,2,3,4,5]

a.fill(255, 2,2) #=> [1, 2, 255, 255, 5]
a.fill(0, 1..2) #=> [1, 0, 0, 255, 5]
{% endhighlight %}

### 清空数组
{% highlight ruby %}
a = [1,2,3,4,5]
a.clear #=> []

p a #=> []
{% endhighlight %}

### 数组连接
可以使用array#+或者array#concat方法将多个数组连接
{% highlight ruby %}
a = [1,2,3,4,5]

p a + [10, 20] #=> [1, 2, 3, 4, 5, 10, 20]
p a #=> [1, 2, 3, 4, 5]
a.concat([10, 20]) #=> [1, 2, 3, 4, 5, 10, 20]
p a #=> [1, 2, 3, 4, 5, 10, 20]
{% endhighlight %}

### 数组的交集与并集
{% highlight ruby %}
p [1,3,5,7] | [2,4,6,8] #=> [1, 3, 5, 7, 2, 4, 6, 8]
p [1,2,3,4] | [3,4,5,6] #=> [1, 2, 3, 4, 5, 6]

p [1,3,5,7] & [2,4,6,8] #=> []
p [1,2,3,4] & [3,4,5,6] #=> [3, 4]
{% endhighlight %}

### 修改数组中多个元素
{% highlight ruby %}
a = [1,2,3,4,5]

a[0...2] = [111, 222, 333]
p a #=> [111, 222, 333, 3, 4, 5]

a[3,2] = [444,555] #=> [444, 555]
p a #=> [111, 222, 333, 444, 555, 5]
{% endhighlight %}

### 将多维数组转换为一维数组
{% highlight ruby %}
a = [1,[2,[3,4],5],[6,7]]

p a.flatten #=> [1, 2, 3, 4, 5, 6, 7]
a.flatten! #=> [1, 2, 3, 4, 5, 6, 7]
{% endhighlight %}

### 反转数组
reverse

### 过滤重复元素
uniq

### 删除指定位置的数组元素
{% highlight ruby %}
a = [5,1,4,2,3]

a.delete_at(0) #=> 5
p a #=> [1, 4, 2, 3]

a.delete_at(1) #=> 4
p a #=> [1, 2, 3]
{% endhighlight %}
### 删除匹配元素
{% highlight ruby %}
a = ["apple", "orange", "lemon", "apple", "vine"]

a.delete("apple") #=> ["apple"]
p a #=> ["orange", "lemon", "vine"]
a.delete("apple") { |x| puts "#{x} not found" } #=> "apple not found"
{% endhighlight %}

### 查找数组元素
{% highlight ruby %}
a = ["apple",10,"orange",["lemon","vine"]]

p a.index("apple") #=> 0
p a.index(10) #=> 1
p a.index(["lemon","vine"]) #=> 3
p a.index("fruit") #=> nil
{% endhighlight %}

### 搜索多维数组
{% highlight ruby %}
a = [["apple",100],["vine",500],["orange",300]]

p a.assoc("apple")  #=> ["apple", 100]
p a.assoc("orange") #=> ["orange", 300]
p a.assoc("pear")   #=> nil
{% endhighlight %}

## 数组

### reverse_each
对数组进行反向迭代遍历

### map collect
{% highlight ruby %}
array = %w(one two three)
brray = array.map do |item|
  item.upcase
end
# brray = ["ONE", "TWO", "THREE"]
# 等价于
brray = array.map(&:upcase)
{% endhighlight %}
collect的用法和map的用法类似

### inject reduce
inject求数组元素的和  
方法一
{% highlight ruby %}
arr = (1..10).to_a
all = arr.inject(0) do |sum, i|
  sum += i
  #sum + i
end
puts all
{% endhighlight %}

方法二
{% highlight ruby %}
all = (1..10).inject(:+)
{% endhighlight %}
reduce用法和inject用法类似

### select reject
select从数组中筛选元素
{% highlight ruby %}
array = (1..10).select do |item|
  item < 5
end
# array = [1, 2, 3, 4, 5]
{% endhighlight %}
reject从数组中剔除元素,delete_if相当于object#reject!
{% highlight ruby %}
array = (1..10).reject do |item|
  item < 5
end
# array = [6, 7, 8, 9, 10]
{% endhighlight %}

### group_by
{% highlight ruby %}
(1..10).group_by { |item| item%3 }
# {1=>[1, 4, 7, 10], 2=>[2, 5, 8], 0=>[3, 6, 9]}
{% endhighlight %}

### 排序
{% highlight ruby %}
class Node
  attr_accessor :lvl_one, :lvl_two
  def initialize(one, two)
    @lvl_one, @lvl_two = one, two
  end

  def <=>(node)
    if @lvl_one < node.lvl_one
      -1
    elsif @lvl_one == node.lvl_one
      if @lvl_two < node.lvl_two
        -1
      elsif @lvl_two == node.lvl_two
        0
      else
        1
      end
    else
      1
    end
  end
end

arr = []
arr << Node.new(3, 9)
arr << Node.new(9, 3)
arr << Node.new(1, 2)
arr << Node.new(2, 2)
arr << Node.new(2, 2)
arr << Node.new(3, 1)

arr.sort.each do |e|
  puts "#{e.lvl_one}, #{e.lvl_two}"
end
=begin
1, 2
2, 2
2, 2
3, 1
3, 9
9, 3
=end
{% endhighlight %}

### each_with_index
{% highlight ruby %}
(11..20).each_with_index do |number, index|
  puts "index: #{index}, number: #{number}"
end
{% endhighlight %}

### for循环
{% highlight ruby %}
arr = (11..20).to_a
for i in 0...arr.length
  puts arr[i]
end
for i in 1..arr.length
  puts arr[i-1]
end
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

# 其他

## 测试程序时将数据和代码一起写在代码文件中
{% highlight ruby %}
# 两种写法都可以
#DATA.each_line do |line|
DATA.each do |line|
  puts line
end

# __END__后为数据内容
__END__
line1
line2
{% endhighlight %}
