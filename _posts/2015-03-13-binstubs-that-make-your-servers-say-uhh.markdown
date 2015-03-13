---
layout: post
title:  "Binstubs That Make Your Servers Say Uhhhhh"
date:   2015-03-13 12:13:26
categories: binstubs
meta: "How about a two-letter command to boot any server in your myriad projects?"
---
If you work across a variety of projects, remembering local server boot commands
and ENV settings can be tedious. Even if you don't, who wants to type `rails s`
multiple times every day? Maybe you already have shell commands in place, but are
they standardized and aliased so just two letters will boot any project? Here's
my setup:

## Alias
`~/aliases.local`
{% highlight sh %}
alias sr='server'
{% endhighlight %}

## Node Example
`{PROJECT_ROOT}/bin/server`
{% highlight sh %}
#!/bin/sh
PORT=3001 nodemon app.js
{% endhighlight %}

## Rails Example
`{PROJECT_ROOT}/bin/server`
{% highlight sh %}
#!/bin/sh
rails s
{% endhighlight %}

## Jekyll Example
`{PROJECT_ROOT}/bin/server`
{% highlight sh %}
#!/bin/sh
bundle exec jekyll serve
{% endhighlight %}

## Perl Example
`{PROJECT_ROOT}/bin/server`
{% highlight sh %}
#!/bin/sh
perl -d script/server.pl
{% endhighlight %}

Just `cd` into any project and initiate the server with `sr`,
it doesn't get much easier than that. I originally mentioned this in my earlier
screencast about [speeding up your development process][sc], give it a look!

[sc]: http://blog.paulrugelhiatt.com/rails/vim/productivity/2014/12/12/screencast-tips-and-tricks-to-speed-up-web-development-workflows.html
