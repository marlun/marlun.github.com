---
layout: post
title: Getting errors about locale over SSH
categories:
- linux
- osx
---

I recently got a Macbook Air with OS X Lion installed and immediately started getting locale errors when connecting to linux servers through SSH. At first I thought it had something to do with the servers but today I found that Lion seem to have added a line to its `/etc/ssh_config` file which looks like the line below.

	SendEnv LANG LC_*

This instructs the SSH client to send the local variable LANG to the server. Since OSX and some linux servers don't use the same values you get all these noisy warnings. If you remove the line it means that the server you connect to won't pick up your local language settings. I haven't had the time to properly look into this and solve it in any other way than removing the line but at least I don't have to see those warnings.
