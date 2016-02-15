---
layout: post
title:  "A Concurrency Conundrum in Rails"
date:   2016-02-15 12:13:26
categories: rails concurrency
meta: "Ruby is notoriously bad at concurrency, but even Postgres locking seems to fall short of this particular problem."
---

Ruby is notoriously bad at concurrency, but usually we can limp along in
concurrent environments with some combination of thread-safe best practices,
ruby semaphores and database row locking. The latter is particularly effective
for row updates. But what about reads?

Say I have a dangerous `DeathStar` class:

{% highlight ruby %}
class DeathStar

  def fire_laser
    return if laser_fired?
    fire!
  end

  private

  def fire!
    # Fire protocol
    update(laser_fired: true)
  end
end
{% endhighlight %}

Let's assume that we really don't want to fire the laser more than once, because
it costs a ton of Imperial Credit and Vader is strapped. But we have tons of
information coming into the system indicating whether the laser should be fired,
and each one kicks off a redis-backed sidekiq process that runs on workers
across multiple servers:

{% highlight ruby %}
class IntelGatherer

  def new_planet_position(death_star_id)
    # Target planet positions are changing
    FireWhenReadyWorker.perform_async(death_star_id)
  end

  def laser_charge_state(death_star_id)
    # Charge state is changing
    FireWhenReadyWorker.perform_async(death_star_id)
  end
end
{% endhighlight %}

{% highlight ruby %}
class FireWhenReadyWorker
  include Sidekiq::Worker

  def perform(id)
    death_star = DeathStar.find(id)
    death_star.fire_laser
  end
end
{% endhighlight %}

Given the size of the Empire, we're getting tons of data about planets, fleets,
etc. concurrently all the time, so the system is running the firing protocol
more or less at the exact same time across multiple servers. This means if there
is a delay between the `laser_fired?` check and the `fire!` completion then
multiple background workers could make it passed our `return if laser_fired?`
guard statement, and `fire!` will be called multiple times for the same
DeathStar.

The solution to this issue isn't jumping out at me immediately. It seems like
you'd either need a row-level read lock on the database (which sounds weird,
scary and unsupported), or some kind of redis-backed semaphore
(concerning/complicated for similar reasons). Or is the problem here in
the framing of the question, and this pattern shouldn't even be used for this
purpose? I'm curious to hear your thoughts!
