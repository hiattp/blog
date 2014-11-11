---
layout: post
title:  "Vim Tip: Shift Is Overplayed Part 2"
date:   2014-11-11 12:13:26
categories: vim
meta: "Avoid modifier keys in Vim that might slow you down. Here's Part 2 on Shift."
---
As promised, here is round two in my Shift evasion series. I had a slight detour
last week when I discovered a neat [Caps Lock remapping trick][remap] that
remaps both `Ctrl` and `Esc` to one home row key. With Control and Escape out of
the picture I've decided to get a bit more
aggressive on Shift in this round, so this isn't so much a recommendation as it
is an experiment that I'll be undertaking over the next week or so.

One thing that has bothered me lately is that while coding I type special characters far
more than I type numbers. Yet I have to use Shift to access these characters,
which tends to throw off my accuracy. So I'm going to try reversing that for the
next week. Without further ado, here's the latest addition to my `.vimrc.local`
courtesy of the [Vim Tips wiki][wiki]:


{% highlight vim script %}
" map each number to its shift-key character
inoremap 1 !
inoremap 2 @
inoremap 3 #
inoremap 4 $
inoremap 5 %
inoremap 6 ^
inoremap 7 &
inoremap 8 *
inoremap 9 (
inoremap 0 )
inoremap - _
" and then the opposite
inoremap ! 1
inoremap @ 2
inoremap # 3
inoremap $ 4
inoremap % 5
inoremap ^ 6
inoremap & 7
inoremap * 8
inoremap ( 9
inoremap ) 0
inoremap _ -
{% endhighlight %}

This is either going to be incredibly aggravating or incredibly awesome. I'll
let you know.

[wiki]:    http://vim.wikia.com/wiki/Invert_the_number_row_keys_for_faster_typing
[remap]:   http://blog.paulrugelhiatt.com/hacks/apple/2014/11/06/optimize-osx-keymappings-for-web-development.html
