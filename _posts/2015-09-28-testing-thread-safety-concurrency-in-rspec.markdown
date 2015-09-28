---
layout: post
title:  "Testing Thread Safety/Concurrency in RSpec"
date:   2015-09-28 12:13:26
categories: rails rspec
meta: "Test drive concurrency issues in your Rails app."
---

Leveraging Unicorn or Puma servers for concurrency is great until you run into
inexplicable bugs that turn out to be concurrency-related. For example, we have
a token update method in our `User` model that updates a JSON-serialized
`tokens` field representing a hash of auth tokens:

{% highlight ruby %}
def update_tokens(client_id, token)
  tokens[client_id] = {
    token: BCrypt::Password.create(token),
    expiry: (Time.now + DeviseTokenAuth.token_lifespan).to_i
  }
  save
end
{% endhighlight %}

The way [serialization][serialization] works in `ActiveRecord` requires the
existing data to be loaded into memory, the hash modified, then saved to the
database. If you have two requests processing this simultaneously they will each
load the old version of the field into memory, save their new key/value pair
to the old hash, and save their own version of the hash to the database
(with the second update omitting the new key/value pair in the first).

Any good bug fix starts with a reproduction test, but reproducing concurrent
actions in RSpec can be tricky. My solution in this case was to spike a method
call within the action with a new thread, execute that thread while first action
is "in progress," then test for the outcomes of both cases:

{% highlight ruby %}
describe '#update_tokens' do
  it 'is threadsafe', db_strategy: :truncation do
    u = create(:user)
    thread_injected = false
    time = Time.now
    allow(Time).to receive(:now) do
      unless thread_injected
        thread_injected = true
        Thread.new { u.reload.update_tokens('c2', 't2') }.join
      end
      time
    end
    u.update_tokens('c1', 't1')
    expect(u.tokens['c1']).not_to be_nil
    expect(u.tokens['c2']).not_to be_nil
  end
end
{% endhighlight %}

Essentially you find an entry point within the function (a point at which you'd
be concerned if a concurrent process started before it finished), in this case
the `Time.now` call. On the first attempt you run the same function (optionally
on a different thread). Note that you have to switch to a truncation db
cleanup strategy if you are using the default transaction-based approach.

This test fails unless we add a lock to prevent simultaneous requests from
modifying the same record at the same time (lock the record in the database,
reload it in memory, then execute the changes):

{% highlight ruby %}
def update_tokens(client_id, token)
  with_lock do
    tokens[client_id] = {
      token: BCrypt::Password.create(token),
      expiry: (Time.now + DeviseTokenAuth.token_lifespan).to_i
    }
    save
  end
end
{% endhighlight %}

Specs are green and we've eliminated our concurrency issue. If you've addressed
concurrency with another test-driven approach I'd love to hear about it!

[serialization]: http://api.rubyonrails.org/classes/ActiveRecord/AttributeMethods/Serialization/ClassMethods.html#method-i-serialize
