---
layout: post
title: Setting Up a Reasonable MLTon Development Environment in Emacs
---

{{ page.title }}
================

[Standard ML](http://en.wikipedia.org/wiki/Standard_ML) and
specifically Standard ML as compiled by the extremely good
[MLton](http://mlton.org) compiler has become the low level
optimization language for applications written here at 10io. We are a
big user of [Erlang](http://www.erlang.org). In Erlang applications it
is not uncommon for there to be places where some gain can be had from
using faster natively compiled code. In those places, it customary to
extend the Erlang system using C via a
[NIF](http://www.erlang.org/doc/man/erl_nif.html). However, We have
actually started using SML and the same NIF technology to accomplish
this purpose. It does take a very thin shim written in C to get this
done. However, overall we consider this the best available trade-off
between speed of execution and bug free runtime code that we can
get. So far that consideration has proven to be correct.

The benefits of SML as an extension language is the subject for a
future post, though. This post is about setting up a reasonably
productive environment for MLton. In this post we will go over the
following.

1. Getting MLton installed on your system
2. Setting up the sml-mode and mlton-mode in Emacs
3. Setting up your project

This should get you up to speed and building with MLton quickly.

Installing the System
---------------------

### MLton

I suggest you install MLton via your distribution's package
manager. MLton is a very stable platform that evolves slowly. It is
likely that your distribution has pretty up to date packages
available. This is certainly true for Arch, Ubuntu, Fedora, etc. If,
however, you want to install it yourself then you can do so following
the [instructions](http://mlton.org/Download).

### sml-mode

Next you will want to get sml-mode installed. I suggest you do this
through Emac's new package manager [ELPA](http://tromey.com/elpa/) or
[el-get](https://github.com/dimitri/el-get). However, if you want to
install it manually for some reason you can do so. Instructions for
manual setup and install of sml-mode is available
[here](http://mlton.org/Emacs).

### mlton-mode

Finally install mlton-mode. You can do that by following the
[instructions on the MLton website](http://mlton.org/Emacs). Don't
just install just `esml-mlb-mode.el`, make sure you install all the files
in the `emacs` directory of the [svn repo]
(http://mlton.svn.sourceforge.net/viewvc/mlton/mlton/trunk/ide/emacs/)
or if you prefer you can get it from our
[github mirror](https://github.com/afiniate/mlton-mode).

Global Setup
------------

If you followed the directions on the MLton website you should
generally be in pretty good shape. There are still a few things
missing for a 'reasonably productive' environment though. By
reasonably productive, we mean that you get useful and consistent
syntax highlighting (not so hard) and that as you develop and your
code you get errors are highlighted on the fly. These errors should be
highlighted in such a way that you can click on them and open up the
file and line that produced the error. The usual solution for this is
[Flymake](http://flymake.sourceforge.net/) mode. I consider this a
necessity for any rational development. There is some bad news and
some good news about that. The bad news is that MLton doesn't really
work that well with Flymake, at all. There are two reasons for
this. The first reason is that MLton is a slow compiler and the second
is that it can't compile just a single file (as flymake requires),
it needs to compile the entire project. Both of these reasons stem
from the fact that MLton is a whole program compiler. It needs access
to all the source for a project to build that project. Now that we
have heard the bad news, the good news is that there is an alternative
to Flymake produced by the MLton guys and that alternative is the
[Background Build Mode](http://mlton.org/EmacsBgBuildMode). This will
build the project in the background and when the build is complete pop
up a list of Errors and Warnings in the correct buffers.

The Background Build Mode works by having a description (usually a
file called `Build.bgb`) registered with the mode. It then builds all
files related to that mode. In Bg-mode you must manually register the
`Build.bgb` with the mode. I am not a big fan of having to do
something manually every time I open emacs. This is true even though I
generally keep emacs open for weeks at a time. So, because I am
inherently lazy, I wrote the following elisp function to look for a
`Build.bgb` and automatically register it every time we open an sml
file. This means that the background build mode is silently started
correctly and simply works for me for those projects that contain
`Build.bgb` in the project root.

To get the same functionality simply drop this in your .emacs or an
elisp file that gets loaded into emacs.

    (defun my-load-project ()
      (interactive)
      (let* ((dirname (file-name-directory (buffer-file-name)))
            (project-dir (locate-dominating-file dirname "Build.bgb")))
        (if project-dir
            (bg-build-add-project (concat project-dir "Build.bgb"))
          nil)))

Finally, I want to load all of this functionality when an SML file
gets loaded. To do that I add my own mode hook. This hook looks as
follows.


    (defun my-mlton-mode-hook ()
      (flyspell-prog-mode)
      (require 'bg-build-mode)
      (bg-build-mode)
      (my-load-project)
      (require 'compile)
      (add-to-list
       'compilation-error-regexp-alist
       '("^\\(Warning\\|Error\\): \\(.+\\) \\([0-9]+\\)\\.\\([0-9]+\\)\\.$"
         2 3 4))
      (require 'sml-mlton))

This does a few things that you may or may not want to do. I am a
horrible speller so I always want
[flyspell-prog-mode](http://www.emacswiki.org/emacs/FlySpell)
enabled. The next two lines are about loading the bg-build-mode (which
you should have made available when you installed the MLton emacs
mode). Finally, we add the call to load project and set the error
parsing regexp. All of this was described in the information on the
[MLton Emacs Page](http://mlton.org/Emacs).

The last bit is simple to load up sml mode and add the mode hook. We
can do that with the following two calls in our setup elisp

(add-hook 'sml-mode-hook 'my-mlton-mode-hook)
(require 'esml-mlb-mode)

That gives us everything we need to for the global setup of MLton.

Project Setup
-------------

To get the best out of bg-mode you need to have your project setup in
such a way that a single command will build and run the tests If you
don't have a one command build and test the project then *stop what
you are doing right now and fix that massive glaring
problem*. Assuming that you have doen that then all that is left is
adding the `Build.bgb`. This is a matter of adding the file and filling it
with some information about how that project should be built. The
Build.bgb for the 10io myrmas project looks as follows.

    ;; -*- mode: Lisp; fill-column: 80; comment-column: 75; -*-
    (bg-build
     :name  "Myrmas"
     :shell "nice -n5 make all")

It should contain the name of the project (that helps identify the
buffer in emacs and the command used to build the project) and the
shell command used to build it. In this case, we have a makefile with
an `all` rule that does everything we need. We wrap it in the `nice`
command to make sure its a non-intrusive background task. you can
follow this exact model for your projects as well.
