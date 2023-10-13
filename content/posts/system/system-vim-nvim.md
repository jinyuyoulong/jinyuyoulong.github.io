---
title: "System Vim Nvim"
date: 2023-10-12T10:32:29+08:00
categories: [system]
tags: [vim]
---

# nvim 的使用探索

> 介绍 nvim 是 vim 的现代改进版，目的是成为一个键盘友好的编辑器

我的插件管理器 vim-plug
我安装的插件: `.vimrc`

```sh
call plug#begin('~/.vim/plugged')

Plug 'mhinz/vim-startify'
Plug 'lfv89/vim-interestingwords'
Plug 'tpope/vim-fugitive'

Plug 'godlygeek/tabular'
Plug 'SirVer/ultisnips',{'for':'markdown'}
Plug 'mzlogin/vim-markdown-toc'

Plug 'plasticboy/vim-markdown'
Plug 'iamcco/markdown-preview.nvim'
call plug#end()
`
```

常用tips
关闭 tab
