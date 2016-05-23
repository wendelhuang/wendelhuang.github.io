---
layout: post
title:  "My Vim experience"
date:   2016-05-22
categories: tools vim
---

* 目录
{:toc}

***

# vim配置

## .vimrc
{% highlight bash %}
set cindent
set smartindent

set tabstop=2
set softtabstop=2
set shiftwidth=2
set expandtab

syntax on
set number
set hlsearch
set showmatch

filetype on
filetype indent on

autocmd FileType python set omnifunc=pythoncomplete#Complete
autocmd FileType javascript set omnifunc=javascriptcomplete#CompleteJS
autocmd FileType html set omnifunc=htmlcomplete#CompleteTags
autocmd FileType css set omnifunc=csscomplete#CompleteCSS
autocmd FileType xml set omnifunc=xmlcomplete#CompleteTags
autocmd FileType php set omnifunc=phpcomplete#CompletePHP
autocmd FileType c set omnifunc=ccomplete#Complete

if has('mouse')
  set mouse=a
endif
{% endhighlight %}

# vim使用大法 
