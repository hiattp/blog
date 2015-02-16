---
layout: post
title: "Introducing Dragon.rb: An Open Source Ruby API for Voice Recognition Software"
date:   2015-02-16 12:13:26
categories: dragonrb ruby
meta: "Making Nuance's Dragon Dictate for Mac extensible enough for programming and other advanced computer interactions"
---
Voice recognition technology seems to be on the rise in both sophistication
and popularity, controlling your phone, your car and your Xbox for those
self-confident enough to talk to their devices without feeling foolish. But
today's Siri seems light-years away from being a productive asset in software
development; or did until I saw Tavis Rudd demonstrate voice-based control of
Emacs at [Pycon 2013][pycon].

Unfortunately Tavis was developing on Windows and had the advantage of
[Dragonfly][dragonfly], so there isn't a great way to build on his progress
if you are an OSX user running Vim. But if you have read any of my other
[blog posts][other] you know that I'm a huge fan of productivity hacks, and I
genuinely think that voice recognition has a future in faster, more productive
web development.

To this end I've started a new experimental open source project called
[Dragon.rb][dragon]. The goal is a simple Ruby-based DSL
for building the complex commands necessary for high-performance
text editing in Dragon Dictate for Mac. Collaborators are welcome and demos are
forthcoming!

[pycon]: https://www.youtube.com/watch?v=8SkdfdXWYaI
[dragonfly]: https://github.com/t4ngo/dragonfly
[other]: http://blog.paulrugelhiatt.com/rails/vim/productivity/2014/12/12/screencast-tips-and-tricks-to-speed-up-web-development-workflows.html
[dragon]: https://github.com/lockstep/dragon.rb
