---
layout: post
title: Cut out those columns in vim
categories:
- vim
- unix
---

If you ever end up with a file looking something like the following and only
want the second column, don’t start doing a macro or anything fancy.

	Date,Title,Comments
	2015-02-01,Simple use of cut in vim,5
	2015-02-05,Extreme weather indoors,3
	2015-02-10,Cars don't need wheels,8

All you need is the cut utility and a filter command.

	:%!cut -d , -f 2

Where `-d ,` defines that out delimiter is comma and `-f 2` that we want the
second field (since the column numbering starts at 1). If your lines are
separated by white space (maybe a TAB) you don’t even need the -d.

	:%!cut -f 2

If you only want a couple of lines, select the lines you want and hit `:` and
you’ll get the correct range.

	:'<,'>!cut -f 2
