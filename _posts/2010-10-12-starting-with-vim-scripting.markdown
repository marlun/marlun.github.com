---
layout: post
title: Starting with vim scripting
---

{{ page.title }}
================

I've pushed my first [vim plugin](http://github.com/marlun/vim-gotobuffer) which I called gotobuffer to Github. It's a buffer switcher which shows you a list of all your open buffers and then lets you filter it by writing a pattern. The idea is that it will work pretty much as [Command-T](http://github.com/wincent/Command-T) does but for opening loaded buffers instead of files.

It's very much in the alpha state and if you try it out your doing so on your own risk. It can do the basics of actually showing a list of all your loaded buffers, let you filter it using a vim pattern (compared using `=~`) and open the selected file. I'll be working on changing the filtering to using a fuzzy search algorithm.

I'd love all the constructive feedback that you can give on how I can make it better, faster or easier to understand.

<p class="date">12 October, 2010</p>
