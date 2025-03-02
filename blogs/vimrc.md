---
layout: page
permalink: /blogs/vimrc/index.html
title: vimrc
---

<br>" 打开语法高亮
<br>syntax on

<br>" 显示行号
<br>set nu!

<br>" 支持使用鼠标
<br>set mouse=a
<br>set selection=exclusive

<br>" 在状态栏显示光标当前位置
<br>set ruler
<br>" 在状态栏显示当前状态（输入模式或插入模式）
<br>set showmode
<br>" 开启状态栏信息
<br>set laststatus=2
<br>" 显示输入的命令
<br>set showcmd

<br>" 设置终端类型，比如常见的 xterm
<br>set term=xterm

<br>" 设置自动缩进宽度为 4
<br>set shiftwidth=4
<br>" 设置 tab 制表符所占宽度为 4
<br>set tabstop=4
<br>"自动对齐（继承前一行的缩进方式）
<br>set autoindent

<br>" 高亮显示匹配的引号和括号
<br>set showmatch
<br>" 匹配括号高亮的时间（单位是十分之一秒）
<br>set matchtime=1

<br>" 引号，括号自动匹配
<br>inoremap ' ''
<br>inoremap " ""
<br>inoremap ( ()
<br>inoremap { {}

<br>" 高亮显示当前行
<br>set cursorline

<br>" 设置字体
<br>set guifont=Monaco\ 12

<br>" 开启折叠功能
<br>set foldenable
<br>" 用语法来定义折叠
<br>set foldmethod=syntax
<br>let fortran_flod=1

<br>"启用自动补全
<br>filetype plugin indent on
<br>"针对不同的文件类型加载对应的插件
<br>filetype plugin on
<br>"针对不同的文件类型采用不同的缩进格式
<br>filetype indent on

<br>"设置文件编码，避免中文乱码
<br>set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1
<br>set enc=utf8
<br>set fencs=utf8,gbk,gb2312,gb18030
