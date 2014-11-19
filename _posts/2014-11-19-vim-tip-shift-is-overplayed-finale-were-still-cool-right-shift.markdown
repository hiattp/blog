---
layout: post
title:  "Vim Tip: Shift Is Overplayed Finale - We're Still Cool, Right Shift?"
date:   2014-11-19 12:13:26
categories: vim
meta: "Avoid modifier keys in Vim that might slow you down. Except maybe shift..."
---
I've been down on Shift lately in this three-part series that began when I
[remapped my semicolon][first] to decrease my Shift use (which has been great).
Part 2 saw a more aggressive experiment where I tried to
[remap my number keys][second] in
reverse, with the assumption that I use my special characters
way more often than I use numbers while programming, and the results are in!

I had read about people swapping number keys like this, and I found the
relevant `vimrc` snippet on the [Vim Tips wiki][wiki] so I didn't feel too far off the
reservation. But I also hadn't seen a lot of follow-up posts, so for anyone else
considering this here's my advice: **Don't**.

### Some important plugins depend on the default key-mapping

The first thing I didn't anticipate was that some of my most treasured plugins
(namely `jiangmiao/auto-pairs`) stopped working. I probably could have hacked
around and fixed this, but the easiest solution was to undo the remap of my
parentheses keys and write those off as a loss. This meant, however, that now
1-8 was reversed and 9+ was not (more to keep in the brain while coding).

### Numbers are used *way* more frequently than I thought

This was a classic case of taking something for granted. It is true that in
Vim's insert mode you type special characters much more frequently than numbers,
but I didn't appreciate until this week how much numbers are used relative to
special characters in normal mode. This means you have to get used to
thinking differently about the number row depending on the mode you are in, which
is more brain power than I want to use.

But the other interesting phenomenon I noticed was that when you type numbers in
insert mode, you are way more likely to type them in a series. Special
characters on the other hand are most likely typed individually (amongst other
text or before a space). This means that while special characters come
faster and more accurately, numbers in series (the more common case) are way
more difficult to type, which turns out to be a net loss.

### Some introspection

I've come to appreciate that Shift has a well-deserved role here in a
traditional keyboard layout, and I've realize that the typing deficiencies
leading me to this remap were largely due to my improper use of the correct
shift key (e.g. using left Shift for the `#`). So my new solution is to correct
that behavior, not the mapping of the keyboard, by deactivating keys that use
the improper Shift combination. My guess is that training out the bad habit will
solve the special key problem way more effectively than this failed remap.


[first]:   http://localhost:4000/vim/2014/10/28/vim-tip-shift-is-overplayed-part-1.html
[second]:  http://localhost:4000/vim/2014/11/11/vim-tip-shift-is-overplayed-part-2.html
[wiki]:    http://vim.wikia.com/wiki/Invert_the_number_row_keys_for_faster_typing
