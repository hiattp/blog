---
layout: post
title:  "Essential Vim Plugins"
date:   2014-10-22 12:13:26
categories: vim
---
I [wrote previously][previous] about basing [my setup][overrides] on the
[thoughtbot][thoughtbot] dotfiles. They include some critical plugins by
default:

{% highlight ruby %}
Plugin 'christoomey/vim-run-interactive'
Plugin 'croaky/vim-colors-github'
Plugin 'kchmck/vim-coffee-script'
Plugin 'kien/ctrlp.vim'
Plugin 'pbrisbin/vim-mkdir'
Plugin 'scrooloose/syntastic'
Plugin 'slim-template/vim-slim'
Plugin 'thoughtbot/vim-rspec'
Plugin 'tpope/vim-bundler'
Plugin 'tpope/vim-endwise'
Plugin 'tpope/vim-eunuch'
Plugin 'tpope/vim-fugitive'
Plugin 'tpope/vim-rails'
Plugin 'tpope/vim-repeat'
Plugin 'tpope/vim-surround'
Plugin 'vim-ruby/vim-ruby'
Plugin 'vim-scripts/ctags.vim'
Plugin 'vim-scripts/matchit.zip'
Plugin 'vim-scripts/tComment'
{% endhighlight %}

I'd argue that some of these are a bit too environment-specific to warrant
global inclusion but hey, I trust their judgement. I use an additional set, some
of which I couldn't live without. Here are the top five:

### 1. Search

Even though our `.vimrc` forces grep to use `Ag` when available, I like to
include both the `Ack` and `Ag` plugins in case the Silver Searcher isn't
available (and I like the `:Ag` command).

    Plugin 'mileszs/ack.vim'
    Plugin 'rking/ag.vim'

### 2. Tab Completion

This is a must have, and Supertab does a great job.

    Plugin 'ervandew/supertab'

### 3. Snippets

I love typing `div.<Tab>row<Tab>` and suddenly being inside a new Bootstrap
row div ready for content. I'm not one to compare, but if you liked
Textmate's autocomplete you're going to love these plugins.

    Plugin 'garbas/vim-snipmate'
    Plugin 'honza/vim-snippets'

### 4. Ruby Text Objects

Obviously only important if you write a lot of ruby, but Vim users know the
importance of text objects and this one is critical for productive ruby
development.

    Plugin 'nelstrom/vim-textobj-rubyblock'

### 5. Character Pairs

Forget trying to hack your own character pair completion in `.vimrc`. This
plugin does a great job intelligently autocompleting all of your (), [], "", etc
pairs.

    Plugin 'jiangmiao/auto-pairs'

I have a handful of other plugins in my [local bundles dotfile][bundles], feel
free to poke around or suggest more!

[thoughtbot]: https://github.com/thoughtbot/dotfiles
[overrides]:  https://github.com/hiattp/dotfiles
[bundles]:    https://github.com/hiattp/dotfiles/blob/master/vimrc.bundles.local
[previous]:   http://blog.paulrugelhiatt.com/vim/2014/10/21/lets-make-vim-approachable.html
