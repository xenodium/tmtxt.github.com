---
layout: post
title: "Conkeror   Getting started   Part 1"
description: ""
category: 
tags: []
---
{% include JB/setup %}

**__Conkeror Installation __**

Of course, the very first thing when we want to use a software is to install it. Conkeror is based on XULRunner, which is the core of Firefox, too. There are two ways that we can run Conkeror on our computer. First, install it using XULRunner. The other way is to install it based on Firefox. Conkeror is just like a GUI, and it run based on the XULRunner or Firefox. So if we want to use Conkeror, we need 2 things, Conkeror and either XULRunner or Firefox. Here is the comparison between 2 methods:

Install using Firefox

    - Conkeror is automatically updated when Firefox is updated.

    - Can not set Conkeror as default browser on Mac OS but it is possible on Ubuntu, I don't know on windows since I don't use Windows anymore :LOL:

Install using XULRunner

    - Have to manually update Conkeror when Firefox is updated (on Mac OS), especially now Firefox releases new version too fast. I didn't test it on Ubuntu but I saw the command so I thought it can be updated automatically.

    - Can set Conkeror as default browser on MacOS. Again, I need someone to test it on other OS for me!

 

So if you are using Ubuntu, I recommend you to install it based on Firefox. On Mac OS, it's up to you but I install it using Firefox, too since I always open Conkeror everytime I start my computer. And in this article, I will show how to install it on Firefox. For the other method, if you want, you can find the guide on Conkeror's homepage. The link is at the end of this article.

 

*Update*: I thought someone has fixed the problem that we can not set Conkeror as the default browser on MacOS when we install it using Firefox but I haven't tested it yet. I will update soon when I have time to try it.

 

*Note*: There is currently a problem with the downloading system if you are using Firefox/XULRunner version 14 or above (now the XULRunner and Firefox have the same version number), so if you don't mind, just install the lastest Firefox/XULRunner version and enjoy Conkeror. Otherwise, I advise you to install Firefox/XULRunner 12 bacause Firefox/XULRunner 13 is rubbish. Don't worry too much since Firefox/XULRunner releases the new version too fast so there are little changes in each version ;) Just use the 12 version, it is adequate, and wait until someone fix it and contribute the Conkeror or you can be the hero ;)

 

## Preparation:  

Here is the list of things you need to prepare in order to run Conkeror

Firefox, again I recommend Firefox version 12 ;)

Git, you need git to obtain conkeror source code. Please, forget the SVN. I hate it anyway :LOL:

 

## Installation:  

First, you need to obtain Conkeror from the repo, open up Terminal and type this at the prompt. Remember you need to have git installed before.

    git clone git://repo.or.cz/conkeror.git

Alternatively, you can download a snapshot archive from this link: http://repo.or.cz/w/conkeror.git?a=snapshot;h=master;sf=tgz and then extract it

I recommend you to use git to clone that repo cause it's easy to update conkeror.

 

After cloning the repo or extracting the archive, open up the directory where you've just cloned/extracted conkeror, you will see a file named application.ini.

 

Open up terminal again, type this at the prompt

    firefox --app /path/to/application.ini

In that command above, firefox is the command to run your Firefox browser. On windows, it's usually the path to firefox.exe file. On MacOS, open finder and browse to your Firefox.app location, right click on it -> Show Package Contents, continue to go to folder Contents->MacOS, there is a file named "firefox" there. Drag and drop it into your terminal, and continue to type the rest "--app /path/to/application.ini". On ubuntu, if you have firefox loaded into your $PATH, simply type firefox.

/path/to/application.ini to the path to the application.ini file I mentioned before.

 

Hit Return (Enter on Windows) when you're done and see the magic ;)

 

Conkeror should appear and there should be something looks like this

![Conkeror Main Window](/images/2012-12-24-conkeror-getting-started-part-1/conkeror-main.png) 

The installation steps look complicated when you first time see it. But in fact it's just one command: firefox --app /path/to/application.ini. Call firefox and pass the application.ini path as the argument and you're ready to run Conkeror

 

## Automate it:

Instead of typing that command everytime you want to launch conkeror, simply just give it an alias in your shell config. If you're on MacOS, you can use Automator. For the other OS, if you know anyway to automate it, you're are welcome to contibute.

 

Now Conkeror is ready to run on your computer. If you want, you can the the tutorial that you see or you can close it now and wait for my next post :LOL:

 

Conkeror Homepage: <http://conkeror.org/>
My conkeror on github: <https://github.com/tommytxtruong/conkerorrc>
Follow me and we can exchange the experience.