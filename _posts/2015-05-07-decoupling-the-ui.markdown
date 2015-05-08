---
layout: post
title:  "Decoupling the UI - Intro"
date:   2015-05-07 12:13:26
categories: rails
meta: "UIs are becoming increasingly heavy and self-sufficient. What happens when it becomes completely independent in a Rails application?"
---

There has always been a conceptual dichotomy between the front end and the back
end of a typical web application. The back end is where all the business logic
happens while the front end displays the result in a  visually palatable way.
But the distinction in traditional systems has been more or less
abstract in that the UI (the front end) has depended on the back end
for rendering and likewise the back end has depended on a specific front end
implementation (e.g. injecting logic or data directly into views at render
time). The separation has been logical, not technical.

Contemporary applications take this separation a bit further. Modern front end
frameworks (think AngularJS, EmberJS, React, etc) are more than capable of the
necessary front-end logic, and widespread adoption of best-practice API
consumption (usually built on simple JSON data feeds) enables the UI to
consume data asynchronously from separate servers instead being populated
during render time. This means that a true technical decoupling of the UI
from the back end is feasible, and given the user experience and performance
gains it seems like a complete separation of the two is a no-brainer.

But what do we mean by a complete separation, and how practical is it?
Are we still serving an `index.html` file from our API server just to bootstrap
the UI? Are the assets still managed within the API server's tool chain (e.g. the
asset pipeline on Rails), or are we talking about completely separate
repositories and truly client-agnostic "data-only" servers? Companies
at scale are already splitting out components of their apps into
web services, usually breaking up existing monolithic servers. But what about
new builds? Does it make sense to attempt this separation from the beginning of
the product life cycle?

As it turns out a true decoupling at day one is still fairly challenging and
awkward.  Despite the incredibly fast-moving trend towards separation (and lots
of hype around it "in theory") the actual nuts/bolts/workflow of managing
separate, completely agnostic UI/backend applications for a single project can
be painful compared to the mature, streamlined traditional approach. Right as
everyone perfected the art of cranking out big Rails applications in incredible
time frames, we're heading again into the land of limited scaffolding and
nascent best practices (which is great; no lamentation intended).

At [Lockstep][lockstep] I've tackled a few projects recently with various
degrees of a decoupled front end, generally for clients that know they
will need a mobile application but want to build the web version first. This
post is an introduction to a series about decoupling the UI using a
Rails stack and various client side libraries (mainly Angular and React), the
challenges we've faced and how we overcame them. Hopefully this will help
deepen your understanding about hidden costs associated with this architecture,
potentially hidden benefits, and general tips/tricks related to managing peer
applications from editing workflows to test suites to CI and deployment.
Subscribe and stay tuned; feel free to share your own trials and tribulations
in the comments!

[lockstep]: https://www.locksteplabs.com/
