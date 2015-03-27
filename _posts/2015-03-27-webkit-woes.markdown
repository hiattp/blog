---
layout: post
title:  "WebKit Woes"
date:   2015-03-27 12:13:26
categories: rails testing capybara
meta: "Some snags in Capybara WebKit led us to seek other options; here are the gotchas we've recently discovered."
---

I've been a longtime user of [capybara-webkit][webkit] as my Capybara driver,
but as we've been doing more advanced front end UX and single-page apps with
JavaScript we've run into a few issues that forcibly switched us to
[Poltergeist][poltergeist] or other workarounds on a few client projects.
If you are using capybara-webkit here are a couple gotchas in the current
version:

### No support for the body of PATCH requests

This has been a long-term issue as PATCH grew in popularity with Rails 4's
introduction of PATCH as the preferred update method (versus PUT).
We've seen a massive increase in popularity of Rails as a JSON
service feeding data to various clients (mobile, JS MVX frameworks, etc), which
means our integration tests need to drive JS-based applications that are
frequently sending PATCH requests with updated object data. Unfortunately the
Qt WebKit [didn't support bodies in these requests][qt] until the relatively
recent 5.4.1 release.

While the latest version of [PhantomJS][phantom] has picked up the latest Qt,
capybara-webkit is lagging with [this (currently open) issue][issue]. I'm
confident they'll get that fixed sometime soon, but until they do I don't want
to restructure my API methods (revert to PUT) just because of lagging Qt support
in my test driver. And this is nothing against the fab team at thoughtbot, just
the overly transient [nature of tech][why].

### An apparent lack of hand/eye coordination

This hilariously frustrating [issue][hand] isn't limited to capybara-webkit.
Apparently headless browsers have a hard time clicking moving targets,
causing tests to fail intermittently due to false positives when the browser
"thinks" it clicked something and missed. Here is a screenshot from a
"successful" click:

![Falling Knives]({{ site.url }}/assets/falling_checkbox.png)

You can trigger a click event manually with JS but first you have to figure out
why your test is failing, which will likely be a multiple hour endeavor if you
haven't seen this before.

[webkit]: https://github.com/thoughtbot/capybara-webkit
[poltergeist]: https://github.com/teampoltergeist/poltergeist
[qt]: https://bugreports.qt.io/browse/QTBUG-42456
[phantom]: http://phantomjs.org/
[issue]: https://github.com/thoughtbot/capybara-webkit/issues/553
[why]: http://favstar.fm/users/_why/status/3389695893
[hand]: https://github.com/teampoltergeist/poltergeist/issues/280
