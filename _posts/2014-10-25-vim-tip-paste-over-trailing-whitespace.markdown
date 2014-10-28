---
layout: post
title:  "Vim Tip: Paste Over Trailing Whitespace"
date:   2014-10-25 12:13:26
categories: vim
---
If you use [SnipMate](https://github.com/garbas/vim-snipmate) (highly
recommended) you may frequently end up with this situation. Let's say you are
extracting a method in a ruby file, so you need a new
method but you intend to copy some lines from the original.
You might start by typing `def<Tab>my_new_method<Esc>` with the following result:

{% highlight ruby %}
def my_new_method
··
end
{% endhighlight %}

But now when you paste your original lines you'll have to go back and delete
the SnipMate-generated line with its trailing whitespace. I've never wanted to keep
a line with trailing whitespace when pasting over it, so I use the following
in my `.vimrc`:

{% highlight vim script %}
" Paste over lines with whitespace (common when using snipmate)
nnoremap <expr> p getline('.') =~? '\v^\s+$' ? "\"_ddP=`]" : "p=`]"
{% endhighlight %}

Essentially this says *upon (p)ut if the line only contains trailing whitespace,
dump the line into the black hole register and (P)ut*. The extra characters
after the put command are just there to auto-format, so if you are pasting code
that was indented differently it will adjust based on its new context.
