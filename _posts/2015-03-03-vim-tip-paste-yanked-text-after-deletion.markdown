---
layout: post
title:  "Vim Tip: Paste Yanked Text After Deletion"
date:   2015-03-03 12:13:26
categories: vim
meta: "It sucks when you accidentally delete over yanked text in the default register. Here's a solution."
---
How irritating is it to "lose" your yanked text when you make a minor change or
deletion and it overwrites your default register? A recent [Upcase tweet][tweet]
suggested using named registers, but why should you have to think so far ahead
and type extra characters when you are simply shuffling around text?

Fortunately everything you yank gets stored both in the default register *and*
the `"0` register (Oooohh). But typing `"0p` is a bit much, so I have the
following in my [dotfiles][overrides]:

    " Put latest yanked text (bypass latest deleted text in default buffer)
    noremap YP "0P
    nnoremap <expr> Yp getline('.') =~? '\v^\s+$' ? "\"_dd\"0P=`]" : "\"0p=p`]"

The idea is simply to use `Yp` to paste the most recent yank, but there is an
extra flourish in there from one of my [previous tips][previous] that will
automatically paste over whitespace and format the result.


[tweet]:  https://twitter.com/upcase/status/572530082411089920
[overrides]:  https://github.com/hiattp/dotfiles
[previous]: http://blog.paulrugelhiatt.com/vim/2014/10/25/vim-tip-paste-over-trailing-whitespace.html
