---
layout: post
title:  "When Should You Test Views and Controllers in Rails?"
date:   2014-11-13 12:13:26
categories: ruby rails testing
meta: "Many 'pragmatic' Rails developers avoid view and controller tests altogether. I'll make an argument for a more nuanced approach."
---
If you've gotten serious about testing your Rails application and you prefer
RSpec syntax you may have bumped into [betterspecs.org][better]
and this [controversial][debate] aside:

> Deeply test your models and your application behaviour (integration tests).
Do not add useless complexity testing controllers.

This statement captures a sentiment that plagues Rails testing at large. Rubyists
love hard-and-fast rules or robust guiding principles, especially because it
helps the thriving novice community get up to speed on OO design quickly (think
SOLID and [Sandi Metz' rules][sandi]). The problem when applied to testing is
that knowing when and what to test requires a lot more personal judgement (or
preference), and unlike application code tests have a heavily
weighted human component: They only work if they are well maintained and
run regularly.

You see another example of this rule mentality in test coverage percentages. I
frequently hear things like "we try to maintain a 90% coverage rate," which is
measured by some gem like [simplecov][simplecov]. These tools have their place
(particularly in non-TDD rescues), but to use them as part of a new build
completely misses the point of TDD (by definition, you should have 100% "coverage").
And generally a raw coverage rate doesn't matter nearly as much as ensuring that
at some point an automated test runs every piece of production code somehow to
confirm the user's expectations.

### As a general rule, be skeptical of general rules

When it comes to testing, learn to be comfortable with a bit of ambiguity. Here
is an example where you might see such ambiguity, and some decision pathways
that will surface as a result. Let's say we need to display a feed of titles and
summaries from user blog posts:

{% highlight ruby %}
# Controller

def index
  @posts = Post.all
end
{% endhighlight %}

{% highlight erb %}
<%# View %>

<% @posts.each do |post| %>
  <h1><%= post.title %></h1>
  <p><%= post.body %></p>
<% end %>
{% endhighlight %}

{% highlight ruby %}
# Feature test

feature 'Blog post index' do
  background do
    @post = create(:post)
  end
  scenario 'user views blog list' do
    visit('/posts')
    expect(page).to have_content @post.title
    expect(page).to have_content @post.body
  end
end
{% endhighlight %}

This is a reasonable-looking feature test, it will run fast enough not to slow
us down (and you could add some stubbing to speed it up). In many cases I think
you would be fine to stop here (we are hitting both the controller and the view
with this test, so no need to duplicate that by testing them individually). But
wait, now the client wants the ability to load more posts with a 'Load more'
link. You probably won't reload the entire page, so you'll want to render a
subset of posts in this view via AJAX instead (we'll ignore the javascript for
the sake of brevity):

{% highlight ruby %}
# Controller

def index
  @posts = Post.limit(5).offset(params[:offset])
  render layout: false
end
{% endhighlight %}

{% highlight erb %}
<%# View %>

<% @posts.each do |post| %>
  <h1><%= post.title %></h1>
  <p><%= post.body %></p>
<% end %>
{% endhighlight %}

{% highlight ruby %}
# Feature test

feature 'Blog post index', js: true do
  background do
    @post = create(:post)
  end
  scenario 'user views blog list' do
    visit('/posts')
    expect(page).to have_content @post.title
    expect(page).to have_content @post.body
  end
end
{% endhighlight %}

Ignore for a couple sentences the fact that we didn't drive these changes with
tests. A few important things have happened here: We've added complexity to the
controller (a query), and since we are loading the view via AJAX we had to add
`js: true` to the feature spec in order to spin up our javascript driver (e.g.
Poltergeist).

How would we have gone about this change in a TDD fashion? Since we are
following the [betterspecs][better] guidelines we would probably have added a
feature spec that stubbed out a list of `Post` objects and used matchers to
determine how many appeared (leading to a complicated expectation).
We might have mocked the controller's query logic in our feature
spec and set an expectation that it was called, then we could push that query
into the model layer and unit test it.

One issue with that approach is you now have a feature spec telling the
controller how to do its job, so it is going to be brittle. But I have a much
less sophisticated complaint: Now that we are loading a headless browser for
the integration test, it is going to SLOW. Stop thinking milliseconds, start
thinking seconds every time you run it. Then think about running it a thousand
times (as you will throughout the build), or running a thousand tests just like it.
You'll slowly start running the test less often, or eventually abandon it completely.

Note we started the TDD process with the goal of avoiding controller tests,
because that's what the cool kids are doing. In many cases, go for it. But
you'll have much faster and more flexible tests in this case if you drop to
the controller level to test the added complexity. In fact, here is another rule
of thumb for you to ignore in many cases: **Test where you will be adding the complexity,
unless a higher-level test makes it redundant.**
And what qualifies as redundant will depend on your judgement.

#### View tests are like Controller tests (when you need them you need them)

Now let's say the blog post bodies are from CKEditor, so they have embedded
html. You only want to display the first 150 characters of the post in the list
summaries, so you'll want the view to strip the html tags, decode the html
special characters, then truncate the body to a short summary at the proper
length. Do you want to try testing that in the slow-running feature spec? Nope.
Can you test it in the controller? Nope. Do you want that much logic untested in
your application? Nope. Welcome to view testing.

### Don't wash your hands of testing genres

Unfortunately testing is something that takes practice and literature, which
beginners generally don't have and don't like respectively. So my suggestion is
as follows: Don't ignore controller and view testing. Get good at them so you
know where they apply, and decide for yourself when they
don't. Then pick up a copy of [xUnit Patterns][xunit] and leave it next to your
computer (purely for show; maybe someday you'll give it a browse).

[xunit]:     http://xunitpatterns.com/
[better]:    http://betterspecs.org/
[debate]:    https://github.com/andreareginato/betterspecs/issues/14
[sandi]:     http://robots.thoughtbot.com/sandi-metz-rules-for-developers
[simplecov]: https://github.com/colszowka/simplecov
