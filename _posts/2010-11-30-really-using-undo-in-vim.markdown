---
layout: post
title: Really using undo in vim
---

{{ page.title }}
================

Looking for a solution to a problem I had with vim I stumbled up on a really great little plug-in called [Gundo](http://sjl.bitbucket.org/gundo.vim/). What it does is that it makes vim's advanced undo features (with branches) stupidly easy to use. Since vim got support for undo branches I've wanted to use it a couple of time and every time I just barely managed to get the result I wanted. Without Gundo you need to use :undolist, g- and g+. With Gundo all you need to do is move over a list and hit `ENTER`. As you move over the undo list there's a preview window which shows you a unified diff of what changes was made since the last undo.

Gundo seems to have taken a lot of its inspiration from another vim plug-in called [histwin](https://github.com/chrisbra/histwin.vim) which seems to do the same thing except that it has taken a more advanced approach. Take a look at both and see which one you like.

As a side note I've also moved back to FuzzyFinder from Command-T for several reasons. First I noticed that FuzzyFinder now has support for Command-T like behavior where it searches the whole project for a file without having to add `**/` to the pattern. [Takeshi](http://www.vim.org/account/profile.php?user_id=12324) calls it CoverageFile mode. The second reason is that it now also support BufferTag mode where it searches for tags in the current buffer only. This makes it fast and easy to move around a large file. And the third and last reason for me moving back to FuzzyFinder was that Command-T requires ruby support, FuzzyFinder doesn't.

Now, get back to coding!

*This post was written __November 30, 2010__ on my way home from work (and a little at home).*
