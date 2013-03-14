---
layout: post
title: "Backup Emacs Packages using Package Manager"
description: ""
category: 
thumbnail: /files/2013-01-06-config-yasnippet-and-autocomplete-on-emacs/thumbnail.png
tags: [emacs, package manager, tutorial]
---
{% include JB/setup %}

Emacs is not only just a simple text editor. It comes with powerful supporting
packages to extend its capabilities. Emacs has the built-in package manager but
you can also install packages manually by downloading, compiling and add them to
the load path. However, what happen if you change to another computer or one day
your computer broken and you have to freshly install it from the beginning? You
will have to reinstall those packages again, and add them to the load-path
manually. Here is a simple solution that will help us automate the installation
process.

# Load Emacs package manager and Add more source

Emacs is not a package manager, and we should load its package manager and also
add more package source for it before using.  
Add this to your .emacs

{% highlight cl %}
;;; Emacs is not a package manager, and here we load its package manager!
(require 'package)
(dolist (source '(("marmalade" . "http://marmalade-repo.org/packages/")
                  ("elpa" . "http://tromey.com/elpa/")
                  ;; TODO: Maybe, use this after emacs24 is released
                  ;; (development versions of packages)
                  ("melpa" . "http://melpa.milkbox.net/packages/")
                  ))
  (add-to-list 'package-archives source t))
(package-initialize)
{% endhighlight %}

Now start emacs and press M-x, type in **list-packages** to see all available,
installed as well as built-in packages. To install a package, simple hit return
when the cursor is on that package and select **Install**.

# Automatically install required packages

Add this piece of code to your .emacs. Replace tmtxt with any namespace that you like.

{% highlight cl %}
;;; Required packages
;;; everytime emacs starts, it will automatically check if those packages are
;;; missing, it will install them automatically
(when (not package-archive-contents)
  (package-refresh-contents))
(defvar tmtxt/packages
  '(package1 package2 package3 package4 package5))
(dolist (p tmtxt/packages)
  (when (not (package-installed-p p))
    (package-install p)))
{% endhighlight %}

Replace **package1 package2 package3 package4 package5** with the packages that
you want. Each package is separated by a space. What those lines code do is that
everytime emacs start, it will check for those required packages. If they are
missing, emacs will automatically install them and add them to the load path.
You don't have to worry about which packages you have installed or where they
are, whether they are in the load path. Emacs will do those stuff automatically
for you.

Those are not my code, just the one I collected.