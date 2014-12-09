---
layout: post
title:  "Encrypt Files Easily With Zsh"
date:   2014-12-09 12:13:26
categories: zsh
meta: "I find it hard to remember the exact command for zipping a single file, so here is a shortcut."
---
I find it hard to remember the exact command for creating a
password-protected zip file because the source/destination paths are reversed.
Zsh makes it super easy to create helper functions,
so in case anyone else wants to use a more memorable syntax like `encrypt
secrets.txt` here is a simple function:

{% highlight bash %}
function encrypt {
  zip -e "${1%.*}".zip $1
}
{% endhighlight %}

If you are using a setup [like mine][my-setup] you can simply add this in
`~/.zsh/config/post/encrypt` and encrypt away.

[my-setup]: https://github.com/hiattp/dotfiles
