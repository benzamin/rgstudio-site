+++
title = "ShellMamu, Shell Utility Tool"
date = "2016-11-12T21:47:08+02:00"
tags = ["shell", "unix", "terminal", "bash"]
categories = ["Tools", "Utilities"]
banner = "img/blog/shell-mamu.jpg"
+++

[ShellMamu][shellMamugithub] is a small utility/helper tool for [shell][shellref] scripting language. 
It offers some utility commands which I used frequently in my work. The main purpose of shellMamu is to easily provide the needed parameters for a command. 

This document is a brief primer on using [shellMamu][shellMamugithub]. Please visit the [github][shellMamugithub]
page for more details.

<iframe src="https://ghbtns.com/github-btn.html?user=benzamin&repo=shellmamu&type=star&count=true&size=large" frameborder="0" scrolling="0" width="160px" height="30px"></iframe>
<iframe src="https://ghbtns.com/github-btn.html?user=benzamin&repo=shellmamu&type=watch&count=true&size=large&v=2" frameborder="0" scrolling="0" width="160px" height="30px"></iframe>
<iframe src="https://ghbtns.com/github-btn.html?user=benzamin&repo=shellmamu&type=fork&count=true&size=large" frameborder="0" scrolling="0" width="158px" height="30px"></iframe>
<iframe src="https://ghbtns.com/github-btn.html?user=benzamin&type=follow&count=true&size=large" frameborder="0" scrolling="0" width="220px" height="30px"></iframe>

### Background

I've been using small shell/unix commands for various purpose in Mac's [terminal][] for years. Some time ago I was working on some shell scripts for build automation using Jenkins a year back. I found that for a begginer or intermediate experienced developer, its hard to remember all the needed parameters and its order. Sometimes it kills a lot of time, sometime a wrong command can ruin your entire hours work. 

So I decided to write a small utility tool (for myself!) so that the common commands I use can be used more easily. Just you have to type the command in the shellMamu tool and hit enter, and the mamu will ask you politely for all the needed parameters/inputs needed to execute that command. How cool is that? 😎


### Installation

Download or clone [shellMamu][shellMamugithub] repo, open terminal and go to the downloaded/cloned folder using cd command, then run...
<pre><code class="shell">$ sudo sh install
</code></pre>
Note that, mamu needs your admin access/password to get copied in the system folder.



### Basic Usage

**ShellMamu has this available commands:**
```bash
$ mamu help (Prints help for all available commands)
$ mamu countdown (counts down with voice feedback a certain amount of seconds)
$ mamu findnreplace (finds given text and replaces it with a new one in a file)
$ mamu findtext (finds given text in a file or folder and shows a list of them)
$ mamu symboliclink (make a symbolic link of a file/folder into another folder)
$ mamu httpserver (starts basic python HTTP server in a given port & directory)
$ mamu killnode (kills all running node.js instances or a given one)
$ mamu testtls (tests which TLS versions supported on a given website)
```
Just write any command, and mamu will ask you for needed parameters, like-
<pre><code class="shell">$ mamu countdown
</code></pre>
And it'll ask for how many seconds it will countdown...

    ::TIPS:: You can also use countdown command like - $ mamu countdown 10  
     How many seconds you want to countdown? ->  4

And then it starts counting down with voice feedback. You can see all the available commands and help by just typing "mamu" in the terminal.

<iframe src="https://ghbtns.com/github-btn.html?user=benzamin&repo=shellmamu&type=star&count=true&size=large" frameborder="0" scrolling="0" width="160px" height="30px"></iframe>
<iframe src="https://ghbtns.com/github-btn.html?user=benzamin&repo=shellmamu&type=watch&count=true&size=large&v=2" frameborder="0" scrolling="0" width="160px" height="30px"></iframe>
<iframe src="https://ghbtns.com/github-btn.html?user=benzamin&repo=shellmamu&type=fork&count=true&size=large" frameborder="0" scrolling="0" width="158px" height="30px"></iframe>
<iframe src="https://ghbtns.com/github-btn.html?user=benzamin&type=follow&count=true&size=large" frameborder="0" scrolling="0" width="220px" height="30px"></iframe><br>
**Don't forget to star the repo if you like it 😊** 

[shellref]: https://en.wikipedia.org/wiki/Shell_script/
[shellMamugithub]: https://github.com/benzamin/shellmamu/
[terminal]: http://www.macworld.co.uk/feature/mac-software/get-more-out-of-os-x-terminal-3608274/
