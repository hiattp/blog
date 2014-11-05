---
layout: post
title:  "Vim Tip: Shift Is Overplayed Part 1"
date:   2014-10-28 12:13:26
categories: vim
meta: "Avoid modifier keys in Vim that might slow you down. Here's Part 1 on Shift."
---
I don't like to hate on individual keys, but I'm not a huge fan of modifiers in
general and I feel like Shift has a particularly undeserving role as a
participant in every single Vim command (by way of the colon). I'm experimenting
with a few Shift evasion strategies and thought I'd share the progress in a
multipart series.

The first is deliciously short, and found its way into my
`.vimrc` by way of an [@nvie blog post][driessen] (he seems to have picked up the
idea from [@mitsuhiko's dotfiles](https://github.com/mitsuhiko/dotfiles)). Imagine the
possibilities:

    nnoremap ; :

[driessen]:  http://nvie.com/posts/how-i-boosted-my-vim/
