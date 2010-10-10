---
layout: post
title: Local scope variables in vim
---

{{ page.title }}
================

I've been reading up on vim scripting in the last couple of days. When looking at available scripts on github I've seen a lot of code where the `l:` prefix for local scope is used a lot in places where it is not needed an only add to complexity. In functions, variables declared with `let var = value` is made local by default and adding `l:` only makes it look more complex. I believe that one of the most core things to think about when writing code is to make it easy to understand. You can [read more about variables](http://vimdoc.sourceforge.net/htmldoc/eval.html#internal-variables) at the vim online help.

	" Not in a function and needs to be prefixed to be local
	let l:buffer = "value"

	function! functionName()
		" Is in a function and look a lot cleaner without a prefix
		let name = "value"
	endfunction
