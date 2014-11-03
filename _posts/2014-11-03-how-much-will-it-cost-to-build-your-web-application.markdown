---
layout: post
title:  "How Much Will It Cost To Build Your Web Application"
date:   2014-11-03 12:13:26
categories: web-applications cost
---
Having spent years on both sides of the table shopping for web development
services/clients, I've both seen and contributed to the dramatic price swings
you see when requesting proposals for web contract work. I find it incredibly ironic
that internet services make most marketplaces much more transparent, but not the
market for internet services. I want to make a few remarks about why this
phenomenon exists (nothing comprehensive, but hopefully illustrative), give you
a few bottom-line price ranges to justify my search-engine-optimized headline, then
introduce an idea that I think might help equilibrate expectations and remove
some of the mystery surrounding the costs of building your web application.

### Why the huge ranges in cost estimates?

You've probably read about (or experienced) quotes for web development that
ranged from $10K to $100K+ for the same product with the same
requirement specifications. And there are myriad stories across the internet
talking about building websites for $1000 or less. What gives?

#### 1. Web *Sites* and Web *Applications* Are Different

Unfortunately there isn't a great black-and-white distinction between these two
types of internet "products" but there is a huge cost difference between
building a web**site** like [joetheplubmer.com][joe] and dynamic web
**applications** like [Facebook](http://www.facebook.com) or [Twitter](http://twitter.com). One
heuristic you can use to distinguish is that websites primarily display static
content that a website administrator or designer has composed, whereas web
applications are typically processing and rendering content that *users* have
composed. And web applications typically allow users to do more interesting
things than just search and view content. As an example, you've probably used
Wordpress (a web **application**) to compose content for your web**site**.

Now, the cost of a website is driven by the *design* and the *content*, because
you can easily find out-of-the-box solutions to handle the content delivery (servers/hosting). The cost
of a web application is driven by the *complexity* and *scope*, because you will
likely need customized server and view code to process/render the user-supplied
content or actions. Writing this code requires a highly specialized (and
usually expensive) skill set.

You might have website pricing in mind when writing your RFP, but requirements
that fall into web application territory for implementation. My services and
experiences are limited primarily to web applications, so **the rest of this post will only be
applicable to custom web application solutions**.

#### 2. The Internet Looks Easier Than It Is

You've probably never encountered a web application that cost less than $50-100K to
build. Why? Because early web applications (MVPs or low-budget projects) are
limited to a small audience for testing purposes, and only a small minority
achieve widespread adoption. Before web applications scale they *always* go
through multiple costly iterations, and at a certain point require
full-time developers that will clock in around $87K as an [average annual salary][salary]
depending on your location.

When you hear people talk about building an application on the low end of the
price spectrum your selection bias is going to make you think of Twitter on the
cheap, because you've probably never encountered any of the thousands of low-budget
projects that never got traction and warranted additional investment. High-end
proposals typically build in additional time for iterations, additional
resources for design/usability, and additional scalability measures that low-end
proposals will ignore.

#### 3. Long-term Versus Short-term Thinking

In any product as complex as a custom web application, there are literally
thousands of corners to cut. All you will see as the product owner is the front
end, which frequently represents the least expensive part of the web
application. This means that the *cost drivers are all happening in a black box*.
Low-end proposals are going to avoid things like robust testing frameworks and
best-practice code design principals because the client won't see, understand,
verify or value them.

More established freelancers and development shops *insist* on building these
into their pricing structures, because in the long term both maintenance and "reputational" costs
depend on these hidden but critical components.

#### 4. Complex Products Are Difficult to Estimate

Unfortunately it is hard for humans to estimate time requirements for complex
tasks even if you've done it over and over before (see [Planning fallacy][fallacy]).
Development companies that chronically *underestimate* will eventually go out of
business because they have inflexible cost structures. What remains are
companies who chronically *overestimate* (hence your high bids), freelancers who
can more easily survive underestimation (by losing sleep/time/opportunity but
not money), and offshore companies who have enhanced resilience due to
comparatively low labor costs.

### So Bottom Line, How Much Will It Cost?

Of course, it depends. But I'm more prone than others to toss around numbers as
a way of setting rough expectations, and this is generally what I see in the
market right now. For a straight forward MVP with the average scope/number of
features (e.g. a simple social network), you'll probably pay $10-60K for a good freelancer or small team, and
$50K-150K for a brick and mortar web shop based in the U.S. You'll probably pay
30-50% more for a mobile app, because it is more specialized.

That being said, results will vary and there is still too much
variability/opacity for my taste. I'm interested in building a simple polling
tool that let's people submit anonymous project costs with simple
complexity/satisfaction selections. If there is any interest in something like this pipe up
in the comments and I'll put something together.

[joe]:     http://joetheplumber.com/
[salary]:  http://www.indeed.com/salary/Web-Developer.html
[fallacy]: http://en.wikipedia.org/wiki/Planning_fallacy
