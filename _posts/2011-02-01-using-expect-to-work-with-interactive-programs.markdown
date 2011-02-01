---
layout: post
title: Using expect to work with interactive programs
---

{{ page.title }}
================

At work the other day I needed to create a script which would connect to a server through sftp and download a couple of files. I'm sure there are great tools for doing this and I would love to hear how you would solve it in the comments but for several reasons I needed to use `expect` and `sftp` which were available on the server from which the script would run.

[Expect](http://en.wikipedia.org/wiki/Expect) is a tools for automating working with interactive tools such as fsck, passwd or in my case, sftp. In the most simple case you use `spawn` to start a process, `send` to send input to the process and `expect` to wait for output from the process. In my case it looked something like this:

	#!/usr/bin/expect
	set timeout 600
	spawn sftp -oPort=12345 username@server.tld
	expect "password:"
	send "yourpassword"
	expect "sftp>"
	send "get ./download/* ./files\n"
	expect "sftp>"
	exit

An important thing to know is that by default `expect` **only wait for 10 seconds before silently timing out**. Because I downloaded files which could potentially take more then 10 seconds to download I needed to handle this. After some reading I found that all you needed to do was to add `set timeout <time>` to the script. Setting the time to -1 makes it wait forever.

<p class="date">01 February, 2011</p>
