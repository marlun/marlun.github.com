---
layout: post
title: Better % matching in vim for smarty templates
---

{{ page.title }}
================

I work a lot with [smarty templates](http://www.smarty.net/) at work and one of the things that has irritated me for a while now is that the matchit plugin didn't work in smarty template files. The convention is to name the smarty template files .tpl and vim knows this so it gives the file the filetype 'smarty'. Doing so confuses matchit since it doesn't know what a smarty file is. To solve this all you need to do is add a little code in .vim/plugin/ftplugin/smarty.vim.

	" Taken form HTML.vim in vim runtime files
	if exists("loaded_matchit")
		let b:match_ignorecase = 1
		let b:match_words = '<:>,' .
		\ '<\@<=[ou]l\>[^>]*\%(>\|$\):<\@<=li\>:<\@<=/[ou]l>,' .
		\ '<\@<=dl\>[^>]*\%(>\|$\):<\@<=d[td]\>:<\@<=/dl>,' .
		\ '<\@<=\([^/][^ \t>]*\)[^>]*\%(>\|$\):<\@<=/\1>'
	endif

As the comment says the code is taken from vim's default HTML filetype plugin file.

<p class="date">29 September, 2010</p>
