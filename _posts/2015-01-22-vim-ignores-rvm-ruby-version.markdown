---
layout: post
title:  "Vim Ignores RVM Ruby Version"
date:   2015-01-22 12:13:26
categories: rvm vim rails
meta: "Using RVM to set your ruby version? Rails.vim not working? Here's the fix."
---

If you are using a combination of Vim (or MacVim), Zsh and RVM you might run
into an issue where `ruby -v` in the terminal spits out `ruby-2.2.0` but
you see this message when running **rails.vim** commands in Vim:

    Your Ruby version is 2.0.0, but your Gemfile specified 2.2.0

If you are determined enough you might find [this page][rvm-help], which
describes a few situations and fixes for integrating Vim and RVM,
but the solution to this particular issue is somewhat
buried and unclear. TLDR fix: Add the following line to your `.zshenv` file:

    source $HOME/.rvm/scripts/rvm

This is necessary because Vim isn't going to read the dotfiles where you
sourced RVM initially; [see here][blog] for more info.

[rvm-help]: https://rvm.io/integration/vim
[blog]: https://gabebw.wordpress.com/2010/08/02/rails-vim-rvm-and-a-curious-infuriating-bug/
