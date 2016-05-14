---
layout: post
title:  "小技巧: 使用命令行打开gnome的图片查看软件Image Viewer"
date:   2016-05-14
categories: tools linux image
---

ubuntu下默认打开图片的软件是gnome的Image Viewer，它的另外一个名字叫"eye of gnome(gnome之眼)"  
使用命令行打开该软件的命令就是eye of gnome的首字母连在一起eog  
以下内容摘自[gnome官网]  

You can open a specific file by typing the filename after the eog command:
{% highlight bash %}
eog image.jpeg
{% endhighlight %}

You can open a specific folder by typing the folder name after the eog command:
{% highlight bash %}
eog folder
{% endhighlight %}

To see all the images in a folder at once, you may wish to browse the image gallery.
Open an image in fullscreen mode
{% highlight bash %}
eog --fullscreen image.jpeg
{% endhighlight %}

Open image with gallery disabled
{% highlight bash %}
eog --disable-gallery image.jpeg
{% endhighlight %}

Open image in a new instance
{% highlight bash %}
eog --new-instance image.jpeg
{% endhighlight %}

Open a folder in slideshow mode
{% highlight bash %}
eog --slide-show Pictures/
{% endhighlight %}

[gnome官网]: https://help.gnome.org/users/eog/stable/commandline.html

