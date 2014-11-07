---
layout: post
title:  "Optimize OSX Keymappings for Web Development"
date:   2014-11-06 12:13:26
categories: hacks apple
meta: "Avoid the Esc and Ctrl keys to improve speed and decrease the risk of RSI."
---
You won't be part of the Vim/Emacs communities long before hearing rumblings
and grumblings about the Caps Lock key. What a waste of perfectly good home row
real estate, right? You have to move your entire hand for oft-needed `<Esc>` and contort
your pinky repeatedly for `<Ctrl>` while the seldom used Caps Lock key gloats in its
unwarranted place of prestige. But since I *do* have occasion to type in
uppercase I didn't want to lose the functionality altogether by changing its
modifier behavior to something like `<Ctrl>` in my System Preferences.

I recently stumbled onto an [amazing effort by Steve
Losh][space] to optimize his keyboard setup. I intend to emulate those efforts
but before I invest in a tricked-out mechanical keyboard there was one strategy
in particular that seems both brilliant and necessary, simultaneously solving
the Caps Lock, Control and Escape key location issues. From the post:

> Now the Capslock key on the keyboard does the following:
>
>1. If held down and pressed with another key, it acts like Control.
>2. If pressed and released on its own, it acts like Escape.

Small Yo Dawg moment. So where is the dotfile snippet, of course I want this
awesomeness?? Much to my chagrin, it seems the only way to accomplish this
at the moment without a custom keyboard is third party OSX applications (face palm).
You'll have to install both [Seil][seil] and [Karabiner][karabiner] (and keep
the latter running in the background) to accomplish this upgrade. For now this
seems worth it (at least they are open source), but I'll be looking for ways to
do this via a `.osx` file in the future. If you're still on board, install those
utilities and do the following:

### Seil

In the 'Change the caps lock key' dropdown, check the box and change the keycode
to 80. Follow the instructions in the dropdown to change the default Caps Lock behavior in your System
Preferences.

### Karabiner

After installing, create and run a binstub that looks like this:

{% highlight bash %}
#!/bin/sh

cli=/Applications/Karabiner.app/Contents/Library/bin/karabiner

$cli set repeat.initial_wait 40
/bin/echo -n .
$cli set bilalh.remap.f19_escape_control 1
/bin/echo -n .
$cli set repeat.wait 20
/bin/echo -n .
$cli set remap.simultaneouskeypresses_ss_to_capslock 1
/bin/echo -n .
$cli set parameter.keyoverlaidmodifier_timeout 300
/bin/echo -n .
/bin/echo
{% endhighlight %}

This will do a few things:

1. Remap F19 (the key you mapped to Caps Lock in Seil) to `Ctrl` and `Esc`
2. Remap a simultaneous left and right shift press to the original Caps Lock
   functionality
3. Speed up key repeats
4. Change the "Key Overlaid Modifier Timeout" for reasons I won't get into

Now while running Karabiner you'll have a newly minted home-row key that does the work of both `<Esc>`
and `<Ctrl>` without losing the ability to lock caps.

**Credit:** Kudos to Jason Rudolph for a more [detailed implementation][keyboard] with even more optimizations!

### Caveats

As much as I love this so far, there are some caveats that I need to solve
before I really feel satisfied. First, I don't like having to navigate
OSX-specific GUI tools as part of configuring my environment (it defeats some of Vim's key
benefits in its portability). Second, my mouse seems to be a
bit sluggish when running Karabiner. Maybe there is a setting I missed
somewhere, but it will bother me until I can boost my `com.apple.mouse.scaling`
back around 5.

[rsi]:        http://en.wikipedia.org/wiki/Repetitive_strain_injury
[space]:      http://stevelosh.com/blog/2012/10/a-modern-space-cadet/
[keyboard]:   https://github.com/jasonrudolph/keyboard
[seil]:       https://pqrs.org/osx/karabiner/seil.html.en
[karabiner]:  https://pqrs.org/osx/karabiner/index.html.en
