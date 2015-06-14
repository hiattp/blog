---
layout: post
title:  "Decoupling the UI - Boot Multiple Local Servers with Foreman and Subcontractor"
date:   2015-06-14 12:13:26
categories: rails foreman
meta: "Your Rails API and UI application are now in separate directories. Here's how to run them both in development."
---

You'll be accustomed to using `rails server` or the like to boot your Rails
application in development. With that simple command you have everything you
need, typically running on `localhost:3000`. But if your API and UI are in
separate directories or even separate repositories you'll want a way to boot
them together easily so you aren't navigating around projects just to launch
processes.

You've probably seen or used [Foreman][foreman] if you've ever deployed to
Heroku, or if you use other background services and boot them together with
your development server (e.g. [Sidekiq][sidekiq], [Sunspot][sunspot], etc).
Foreman is awesome at solving just this problem (multi-process management). But
Foreman wasn't designed for processes outside of a single directory, so you'll
need one more piece.

Enter [Subcontractor][subcon], a gem that enables Foreman to manage processes
outside of the Procfile's directory. It is even aware of RVM, if you haven't
switched to rbenv yet ;). Using Foreman and Subcontractor you can put together a
Procfile that will run your API on one port and your UI on another with just one
simple command. Here is an example `Procfile.dev` from a recent project
we're working on at [Lockstep][lockstep]. Enjoy!

    api: subcontract --chdir api -- bundle exec rails s
    sidekiq: subcontract --chdir api -- bundle exec sidekiq
    ui: subcontract --chdir ui -- local_server

[sidekiq]:    http://sidekiq.org/
[sunspot]:    https://github.com/sunspot/sunspot
[foreman]:    https://github.com/ddollar/foreman
[subcon]:     https://github.com/pitluga/subcontractor
[lockstep]:   https://www.locksteplabs.com
