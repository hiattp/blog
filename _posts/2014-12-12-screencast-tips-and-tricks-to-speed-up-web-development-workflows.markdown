---
layout: post
title:  "Screencast: Tips and Tricks to Speed Up Web Development Workflows"
date:   2014-12-12 12:13:26
categories: rails vim productivity
meta: "Here are some tips and tricks that you should be using to speed up your development workflows if you aren't already."
---

One of my [recent posts][recent-post] got into some esoteric hypotheses about why
many developers adopt inefficient development styles and practices, so I wanted to
jump to the opposite side of the theory-practice spectrum and show a few ways I speed
up my daily workflows.

I'm using Vim and working on a Rails project here but the intent is to show
strategies that should be cross-platform and cross-editor---you'll just have to figure out
analogues to achieve the same thing if you aren't using Vim on OSX.

I also want to note that none of this is novel so you've probably seen or heard
of these tools, in which case this is just a nudge to use them if you aren't
already. Enjoy!

<div class="bt-video-container" style="position:relative;padding-bottom:75.00%;padding-top:30px;height:0;overflow:hidden"><iframe width="480" height="360" src="http://www.youtube.com/embed/TFysiX9J-fo?rel=0" frameborder="0" allowfullscreen=""></iframe></div>
\**Apparently 'name' is hard to type while talking, who knew?*

### Tools and Hotkeys Mentioned

- OSX Spotlight to open applications
- [Divvy][divvy] to manage windows
- [Zsh][zsh] as an alternative to a Bash shell
- [CDPATH][cdpath] to navigate into project directories quickly
- Aliases for common terminal commands (you can find mine in my [dotfiles][dotfiles])
- [ctrlp] to navigate within projects
- [New windows][new-windows] by movement in Vim
- [Rails file navigation][rails-vim] (e.g. `:A` to jump into a test file) in Vim
- Snippets with [snipmate][snipmate]
- Full line completion with [supertab][full-line]
- Run tests from Vim with [vim-rspec][vim-rspec]

### Update: New Screencast

If you enjoyed this screencast, check out [Quick and Dirty Vim Macros][new-screencast]!

[recent-post]: http://blog.paulrugelhiatt.com/vim/productivity/2014/12/05/your-natural-tendency-to-observe-progress-is-killing-your-productivity.html
[divvy]: http://mizage.com/divvy/
[zsh]: http://www.zsh.org/
[cdpath]: https://tomafro.net/2009/10/tip-cdpath-am-i-the-last-to-know
[dotfiles]: https://github.com/hiattp/dotfiles
[ctrlp]: https://github.com/kien/ctrlp.vim
[new-windows]: http://blog.paulrugelhiatt.com/vim/2014/10/31/vim-tip-automatically-create-window-splits-with-movement.html
[rails-vim]: https://github.com/tpope/vim-rails
[snipmate]: https://github.com/garbas/vim-snipmate
[full-line]: https://github.com/ervandew/supertab
[vim-rspec]: https://github.com/thoughtbot/vim-rspec
[new-screencast]: http://blog.paulrugelhiatt.com/rails/vim/productivity/2015/01/19/screencast-quick-and-dirty-vim-macros.html
