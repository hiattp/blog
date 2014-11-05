---
layout: post
title:  "A Preface To My Vim Tips"
date:   2014-10-24 12:13:26
categories: vim
meta: "A quick read on my attitude towards dotfiles and context for a forthcoming series of posts about how I optimize mine."
---
Something about fine tuning dotfiles triggers a chemical process in the
brain that demands personal `.vimrc` evangelism, and despite my impending
participation I believe this zeal is a primary barrier to
the sort of [standardization][approachable] I think the Vim community needs.
That being the case, I wanted to preface my vim tip series with a few caveats
and goals.

First, I'll try to steer clear of "best practice" vim customizations that I think
people should (and probably do) already have somewhere in their dotfiles. These
have been written about *ad nauseam* elsewhere, so if you are still using
`C-w, l` to navigate split windows these probably aren't for you. I'm certainly
not claiming novelty, just shooting for things that feel under-appreciated or
experimental. In general
I'll avoid shortcuts and settings in the [thoughtbot dotfiles][thoughtbot] since
those have been battle-tested by their team and well covered. Examples
include remapping your leader, setting line numbers and using `C-l` or `C-h` to
navigate windows:

{% highlight vim script %}
let mapleader = " "
set number
set numberwidth=5
set relativenumber
nnoremap <C-j> <C-w>j
nnoremap <C-k> <C-w>k
nnoremap <C-h> <C-w>h
nnoremap <C-l> <C-w>l
{% endhighlight %}

My [local overrides][overrides] focus mainly on two things:

1. <b>Reducing repetition.</b> A never-ending game of Vim golf, what's not to
   love?
2. <b>Reducing mistakes.</b> Unfortunately I am *not* a great touch typist. Like
   many of my AIM-trained peers I am fast but error-prone, and Vim punishes you
   mercilessly for simple typing mistakes.

My solution to reducing typing errors while maintaining speed is first to
improve my typing skill (this takes time), and second to map common vim
commands in such a way that I don't need to venture into challenging key zones
(*cough* number keys *cough*) as often as I otherwise would. This means that
many of my tips might seem amateurish or superfluous to more experienced
developers with better typing skills, but I think the newest crop of Vim users
will appreciate my little conveniences.

Hope you enjoy!

[approachable]:   http://blog.paulrugelhiatt.com/vim/2014/10/21/lets-make-vim-approachable.html
[thoughtbot]:     https://github.com/thoughtbot/dotfiles
[overrides]:      https://github.com/hiattp/dotfiles
