---
layout: post
title:  "Vim Tip: Automatically Create Window Splits With Movement"
date:   2014-10-31 12:13:26
categories: vim
---
At this point I think everyone probably has "faster window movement"
in their dotfiles:

{% highlight vim script %}
nnoremap <C-j> <C-w>j
nnoremap <C-k> <C-w>k
nnoremap <C-h> <C-w>h
nnoremap <C-l> <C-w>l
{% endhighlight %}

You might even be using "more intuitive" splits:

{% highlight vim script %}
set splitbelow
set splitright
{% endhighlight %}

So what about a bit of mix and match for something that is both faster *and* more intuitive? My Halloween treat to you:

{% highlight vim script %}
" Navigate windows with auto-create if navigating at a window edge

function! s:GotoNextWindow( direction )
  let l:prevWinNr = winnr()
  execute 'wincmd' a:direction
  return winnr() != l:prevWinNr
endfunction

function! s:JumpWithCreate( direction )
  if ! s:GotoNextWindow(a:direction)
    if a:direction == 'h'
      vsplit
    elseif a:direction == 'j'
      split
    elseif a:direction == 'k'
      split
    elseif a:direction == 'l'
      vsplit
    endif
    execute 'wincmd' a:direction
  endif
endfunction

nnoremap <silent> <C-h> :<C-u>call <SID>JumpWithCreate('h')<CR>
nnoremap <silent> <C-j> :<C-u>call <SID>JumpWithCreate('j')<CR>
nnoremap <silent> <C-k> :<C-u>call <SID>JumpWithCreate('k')<CR>
nnoremap <silent> <C-l> :<C-u>call <SID>JumpWithCreate('l')<CR>
{% endhighlight %}

Navigation will work as normal except that when you are at, say, the right edge
of your editor and you navigate to the right it will open a new vertical split
to the right and navigate into it. The same goes for left, up and down.

I frequently find myself creating a new split and using [ctrlp][ctrlp] to open
a new file. You can use `<c-v>` or `<c-x>` to split from ctrlp's find mode,
but if you know you want to split out the result before a search I find it is much more intuitive
(and hence faster) to split first, especially if you are particular about where the
resulting window ends up (and if you are counting, the split-first workflow with
the remappings above only adds one `<CR>` keystroke).

[ctrlp]: https://github.com/kien/ctrlp.vim
