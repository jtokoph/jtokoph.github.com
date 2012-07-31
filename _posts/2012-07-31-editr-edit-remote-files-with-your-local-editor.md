---
layout: post
title: editr - Edit remote files with your local editor
enable_comments: true
---

I'll start off by saying that I've never written a blog post before, but I wanted to [write a little something](/images/no-idea.jpeg) about my latest project: **[editr](https://github.com/jtokoph/editr)**.

### The Project

editr allows you to edit remote files with [TextMate](http://macromates.com/), [Sublime Text 2](http://www.sublimetext.com/2), [Chocolat](http://chocolatapp.com/) and more!

Once installed, you'll be able to use `editr` like you would `mate` or `subl` on the command line. Only now, your remote file will be opened in your local mac editor. [Check out the project on GitHub](https://github.com/jtokoph/editr) and give it a try.

{% highlight bash %}
# Running this on a remote machine will open the editor on your mac
$ editr myfile.txt
{% endhighlight %}

### The Reasoning

Last year, Allan Odgaard <a href="http://blog.macromates.com/2011/textmate-2-0-alpha/">released an alpha version</a> of TextMate 2. For various reasons, which I won't get into here, I didn't want to make the switch to TM2. However, the idea of the <a href="http://blog.macromates.com/2011/mate-and-rmate/">rmate</a> functionality blew me away, and I had to enable it for my install of TextMate 1.

### My Requirements

1. The server would work with TextMate, Sublime Text 2 and Chocolat

    _I hated that rmate only worked with TextMate 2, so how could I deny people that used other editors. (It even works with the OS X default editor, TextEdit.)_

2. The client had to run without installing extra runtimes (ruby, node, python)

    _TM2's rmate included a client script written in ruby. While this works for a lot of people, none of the machines I work with on a daily basis have ruby installed._



### The Solution

The server is written in javascript. I decided to use node because it makes it easy to create a server and because I have a javascript obsession. The server has two simple jobs: return the client script on any `GET` request, and open the editor for every `POST` request.

In order to meet the demands of my second rule, I wrote the client as a bash script using `curl`. I figured every linux machine on the planet should have bash installed. If your server doesn't, I apologize and would be happy to merge a pull request with an alternate client (basic shell?). 

To make it even simpler, you don't even have to copy/paste the client script to the remote machine! If you've already setup the server and port forwarding, just make an HTTP `GET` request:

{% highlight bash %}
$ curl localhost:32123 > ~/bin/editr; chmod u+x ~/bin/editr
{% endhighlight %}

### Contribute

If you decide to write the server in a different language, create an `editr-server.py` or `editr-server.xx` and open a pull request!

### View on GitHub: [https://github.com/jtokoph/editr](https://github.com/jtokoph/editr)

