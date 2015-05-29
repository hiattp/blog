---
layout: post
title:  "Decoupling the UI - Integration Tests"
date:   2015-05-29 12:13:26
categories: rails
meta: "So your Rails API is completely separate from the UI. How will integration tests work?"
---

Welcome to the first installment of [Decoupling the UI][decoupling]! If you're
doing things by the book the first stumbling block you'll hit is integration
tests; here's one way to tackle it.

So you've broken your application in two: A Rails API and a JS-based UI that
is built and served separately. It lives in its own directory (not under the
Rails assets/dependencies) and may even have its own Git repository. But you still
want to be test driven, and that means whole-system integration tests that bring
the two back together are going to be a critical first hurdle. You'll be used to
doing something like this in Capybara:

    scenario 'I access the home page' do
      visit '/'
      expect(page).to have_content 'My Awesome Site'
    end

But now the Rails environment only serves JSON and doesn't know about your
fancy UI elsewhere on your system. And are you sure the integration test
infrastructure should still be running within the context of the API or does it
belong with the UI, or someplace else entirely? Hmm...

There are a few ways to approach this. Your testing architecture could be
completely independent, but that generates a lot of complexity and overhead
you don't need at the moment. And you could run PhantomJS with Karma or the like
to drive tests in a Grunt|Gulp process on the UI side, but what about test setup
and teardown in the database? No, you'll actually want the integration tests to
be coupled to the API so you can easily set up tests with standard
`background` and `context` blocks (if you are using RSpec/Capybara). That solves
one side of the equation, where your tests now have complete access and
knowledge of the API. What about the UI?

One way to make the UI accessible to Capybara is to serve it on a different port
and use fully qualified URLs. There are a few issues with this, but my main one
is speed. Do you want to boot the UI server every time you run a single
test case? Does it spin up and down, or do you leave it running? How is that
going to work on your CI server?

I have a different approach that feels a bit strange but gets the job done
without worrying about separate servers despite a fully decoupled UI. Check this
out:

    ln -s ui/build rails_api/public

Remember that you can configure Rails to serve static content from its `public`
directory, so I just symlink my UI build directory to the Rails public directory
and let Rails pretend the UI is part of its public assets. Now Capybara
will work exactly the same as before, and you can run integration tests as
easily as if the API and UI were unified.

[decoupling]: http://localhost:4000/rails/2015/05/07/decoupling-the-ui.html
