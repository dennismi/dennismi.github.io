---
layout: post
title: "First thoughts of Jekyll"
description: ""
category: 'tutorial'
tags: [trials, jekyll]
theme_name: dmal
---
{% include JB/setup %}
# Installation
Well I am on windows so, i thought, this is gonna be hell. I have seen it before. Looks neat, but way easier to setup on a *nix machine than on windows.

This however was not the case. I found [David Burela's blog](https://davidburela.wordpress.com/2015/11/28/easily-install-jekyll-on-windows-with-3-command-prompt-entries-and-chocolatey/) which details the TWO steps needed.  
Well it may be a little bit more, due to the [chocolatey](http://www.chocolatey.org) prerequisite.

Just in case David Burela's blog is down, and you came here first, let me give you the steps.

1. Have Chocolatey installed? if so jump to 4 if not continue
1. Open command prompt in administrator mode
1. run this command:  
```
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```
   (this is also stated on <http://chocolatey.org>)  
   Chocolatey is now installed
1. Now run:  
```choco install ruby```  
you may need to answer yes a time or two, to allow it to install.
1. reopen the command prompt again. ruby is not yet available.
1. and the final command for getting the jekyll installed is: ```gem install jekyll```

now you have a working jekyll installation.

# First run
So open yet another command prompt. Navigate to you favorite source folder, and enter this:

```
jekyll new <you_blog_name_here>
cd <you_blog_name_here>
jekyll serve
```

Once the command prompt tells you to hit ctrl+c to stop, do not do that :).

Fire up your favorite browser, and type in the url: http://localhost:4000 and that should display you newly created jekyll blog.

This setup make for some fast revs on the site design, and how a post is gonna look when it is published.

# Conclusion
This is perfect if you want a nice simple, and fast platform for a blog.  
But you only want to have this setup, if you are a developer, but who isn't if they have an [GitHub](https://github.com) account :), and are not afraid of either, command line (cmd or powershell), git, and markdown.

If that sounds like your kind of game, then go try it out. Just remember it is meant to be a STATIC SITE GENERATOR, it is just a bunch of HTML files, where Jekyll takes care of the plumbing.

Cheers.

