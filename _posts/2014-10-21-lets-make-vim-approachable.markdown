---
layout: post
title:  "Let's Make Vim Approachable"
date:   2014-10-21 12:13:26
categories: vim
meta: "Vim is notoriously unfriendly to beginners, but extremely powerful for web development. Let's take some steps to help Vim get out of its own way."
---
After a few years of professional experience almost every developer
will need (or at least encounter) Vim. There is nothing quite as frustrating as
opening a "text editor" and not being able to edit text without accidentally
hitting `i` or `a`. Why is such an important tool so unapproachable?

I'd posit three primary reasons:

1. <b>It's complicated as $h#t.</b> Not much to be done about that; you just
   have to crank on [Vim Adventures](http://vim-adventures.com/) for a while.
   It doesn't hurt to read a few [101 Guides][101-guides] as well.
   Most powerful tools have a learning curve; developers understand that better
   than most.
2. <b>Community Angst.</b> Just Google Vim vs Emacs or Sublime vs Vim if you
   aren't already familiar with the elitist dialogue and pyrrhic arguments that eclipse
   the merits of these tool sets and leave would-be learners somewhere between analysis
   paralysis and trepidation. Relax people, these editors aren't going
   anywhere. Start with one and if you don't like it, switch. At least give Vim
   a chance if you haven't already; your life will be easier
   when you `ssh` into your next client's server.
3. <b>Unfriendly Defaults.</b> More on this below.

In my experience, very few people use Vim without heavy customization. Why?
Because out of the box you get virtually nothing but an extremely unintuitive
editor. Think learning Rails without boiler plate code or scaffolding to get you
started. Beginners are encouraged to add things like `set number` to their
`.vimrc` file. Are there a lot of people running around editing files without
line numbers? No. Making a new Vim user add things to a dotfile to achieve
obvious default behaviors seems inane, and valid grounds for premature Vim
abandonment.

> I didn't need these "dotfile" shenanigans with Sublime. Btw,
> why doesn't my cursor work any more?

I think Vim beginners have enough to worry about without trolling [Vim
Tips][vimtips] every time they want to do something obvious. And I wouldn't
limit that to `.vimrc` customization. The magic of Vim happens in the amazing wealth of
plugins, like running specific RSpec tests in two keystrokes [without leaving the
editor][vim-rspec]. And project navigation is truly unbearable
without something like [ctrlp][ctrlp].

It seems to me that beginners should be weaned on a default set
of "customizations" instead of encouraged to learn "normal" behavior
while accumulating their own custom settings through iterative bouts
of hair pulling. And for that matter, do we *all* need to add `set number` and
`set backspace=2` to our `.vimrc`? It doesn't seem terribly DRY as a community.

### How about a little standardization?

Beginners should be introduced to Vim with a standardized set of dotfiles
and plugins; they will start to see the silver lining earlier in an otherwise
harrowing learning curve. But I wouldn't mind seeing even broader adoption of
standardized dotfiles, with individual personalization kept in local overrides.
Besides improving the learning curve this standard dotfile/plugin combination
makes it easier to pair/collaborate, and to pick out useful improvements
while rummaging someone else's setup since you don't have to sort through the
same-old "best practice" chaff.

There are some robust contenders for a "standard", including my favorite dotfile
set by [thoughtbot][thoughtbot] and the somewhat heavy-handed [YADR][yadr]
(even more [here][gdots]).
My own setup uses thoughtbot's as a baseline, so I
can focus more on my [local overrides][overrides] and less on what should be
default behaviors.

[101-guides]: http://computers.tutsplus.com/tutorials/vim-for-beginners--cms-21118
[vimtips]:    http://vim.wikia.com/wiki/Vim_Tips_Wiki
[vim-rspec]:  http://robots.thoughtbot.com/running-specs-from-vim
[ctrlp]:      https://github.com/kien/ctrlp.vim
[thoughtbot]: https://github.com/thoughtbot/dotfiles
[overrides]:  https://github.com/hiattp/dotfiles
[yadr]:       https://github.com/skwp/dotfiles
[gdots]:      http://dotfiles.github.io/
