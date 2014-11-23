---
layout: post
title:  "The MEAN Stack vs Ruby on Rails: Which is right for your MVP?"
date:   2014-11-23 12:13:26
categories: ruby rails mean
meta: "Prospective dev teams are pitching you on Ruby on Rails, MEAN and Django. Here's a nontechnical take on it."
---
I've been approached more and more over the past few months by clients interested in
building version 1.0 of their web application in the MEAN stack. Since the
MEAN acronym is becoming part of the vernacular among "nontechnical" tech
entrepreneurs and product managers, I thought it would be helpful to write a quick post about MEAN
and its place among other popular choices for an MVP (e.g. Rails, Django,
PHP). I won't be getting into the nitty-gritty technical details/trade-offs;
instead I want to add some nuance to your understanding and decision making
process for the next time a dev shop or freelancer pitches you on the wonders of
MEAN relative to more established stacks.

### MEAN vs Rails is Apples and Oranges

In fact it is more accurate to say that comparing the two technologies is
comparing a fruit basket to oranges, since MEAN is actually a series of
technologies: **M**ongoDB, **E**xpressJS, **A**ngularJS and **N**odeJS. MEAN is
being popularized right now as a framework, and in fact the acronym is being
co-opted to mean any stack that has some variation of a Node.js server, a
document-oriented database and a frontend Javascript MVX framework. But here is
something to keep in mind when considering MEAN for your company: MongoDB and
Angular (the M and A of MEAN) can be used in virtually any other technology
stack (Rails, Django, etc). The appropriate comparison if you are considering
MEAN and Rails is actually MEAN versus Rails/Angular/MongoDB (apparently
RAM never caught on).

The point is that you shouldn't be evaluating the relative strengths of MEAN and
Rails directly, because you aren't comparing analogous things. What you
are really evaluating with MEAN is Node/Express as your server framework, which
is going to influence the speed of development, complexity/maintainability of
the code, and the performance of your application.

### Forget Comparative Performance

One thing that really appeals to entrepreneurs considering technology stacks is
the much-hyped performance gains and server efficiency you see with MEAN/Node
due to its "non blocking I/O model" (LinkedIn cut HOW many servers by switching
to Node?? Sign me up!). Here's the dirty secret of custom web applications: The
skill of your developers and the complexity of your application is going to
determine the performance, not the framework. Some frameworks encourage good
behavior more than others, but any time you introduce custom business logic into
a web application you introduce opportunities for performance degradation and
bottlenecks that have nothing to do with the language choice.

### Forget Age/Establishment of the Frameworks

Another compelling motivation to go with the MEAN stack is that it is currently
popular and trendy. There is a strong technological ageism bias in the
pop-technology community, so web shops may tell you something like
"(Rails/Django/etc) is old, the new wave of applications will all be MEAN."
And the basis for this argument is that newer technologies have learned and
overcome the mistakes of their predecessors, and thus have intrinsic
process/framework improvements that allow for better/faster/cheaper development.
For some technology comparisons this is a 100% valid argument, but not this one.
The details are beyond the scope here, but suffice it to say that MEAN is not
going to be simpler or faster to develop in any meaningful way than Rails or Django, so
don't let that argument sway you.

### The Aspects that Matter

At the end of the day there are two main factors that should drive your
decision, in reverse priority order:

1. **The Feature Set**: MEAN and Rails have fundamentally different strengths from a
   feature-set perspective. MEAN is well suited for single page applications
   where not many views need to be rendered, especially if some kind of
   real-time functionality is needed (e.g. a multiplayer game or chat room).
   Rails is better suited in applications that have lots of different object
   types that all relate to each other, like CRMs and social networks.
2. **Whatever an experienced, impartial developer tells you.** More on this
   below:

The inclination of product owners and technophiles at large is to try to
understand the arguments surrounding technology frameworks and strategies
so they feel like they have more control over the destiny of the product and by
extension the company. This is a completely legitimate and advisable pursuit, I
encourage anyone managing a young technology company to learn as much about the
technology as possible. But unfortunately you can't replace years of product
development experience with a few months of reading Quora and tech blogs.

Ultimately framework/stack selection is a very important strategic decision, so
despite your self-education you should seek out someone who has spent the past
few years writing application code or managing builds (preferably across multiple contemporary
frameworks) and describe the product vision. This person cannot be your
prospective developer, since their opinion would be biased by what they can
deliver instead of what is best for your company. So find a friend or pay a
consultant to help you make this decision---it will pay off in spades over the
long term.
