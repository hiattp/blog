---
layout: post
title:  "Rails Admin Custom Action Example"
date:   2014-10-27 12:13:26
categories: ruby rails
---
[Rails Admin][rails-admin] provides a great out-of-the-box Admin portal, and our
clients love it. But like most admin portal solutions it can be difficult to
customize. Rails Admin describes Custom Actions as a core feature, yet I've
found the documentation on this critical workflow to be somewhat lacking, and a
surprising dearth of straight forward examples (come now, let's not create an
entire gem to add a single controller action).

I'll borrow concepts from the original [case study][case-study], while updating
and clarifying the code snippets for a Rails 4 application. My use case
was a link on the User list allowing an Admin to impersonate the user:

### Step 1: Create Your Custom Action Class

There are a bunch of settings related to Rails Admin actions, to include where
the action link appears and what it looks like. We manage these settings by
creating a class for each custom action, and overriding the defaults. Let's keep
our custom action classes their own lib directory:

    lib/rails_admin/impersonate_user.rb

We'll add our custom impersonation settings in `impersonate_user.rb`. I suggest
having the [base class][base-class] handy since we'll be inheriting from it.

{% highlight ruby %}
# lib/rails_admin/impersonate_user.rb

module RailsAdmin
  module Config
    module Actions
      class ImpersonateUser < RailsAdmin::Config::Actions::Base
        # This ensures the action only shows up for Users
        register_instance_option :visible? do
          authorized? && bindings[:object].class == User
        end
        # We want the action on members, not the Users collection
        register_instance_option :member do
          true
        end
        register_instance_option :link_icon do
          'icon-eye-open'
        end
        # You may or may not want pjax for your action
        register_instance_option :pjax? do
          false
        end
      end
    end
  end
end
{% endhighlight %}

### Step 2: Register Your Action

Keep this simple; you don't want to clutter your `rails_admin.rb` initializer.
Since Rails won't know about our new `lib/rails_admin` directory by default,
we'll want to require our new action (or the entire directory) and then
register it:

{% highlight ruby %}
# config/initializers/rails_admin.rb

require Rails.root.join('lib', 'rails_admin', 'impersonate_user.rb')
RailsAdmin::Config::Actions.register(RailsAdmin::Config::Actions::ImpersonateUser)

RailsAdmin.config do |config|
  # Rails admin config
end
{% endhighlight %}

Once Rails Admin knows about the action you can add it to your action list:

{% highlight ruby %}
# config/initializers/rails_admin.rb

RailsAdmin.config do |config|
  config.actions do
    dashboard                     # mandatory
    index                         # mandatory
    # ...other actions...
    impersonate_user              # custom
  end
end
{% endhighlight %}

### Step 3: Custom Action Logic

By default, Rails Admin will render a view with the same name as our action.
This particular application used authentication based on JSON Web Tokens, so
this default behavior was actually what I wanted:

{% highlight html %}
# views/rails_admin/main/impersonate_user.html.erb

<p>Impersonating <b><%= @object.username %></b>...</p>
<script type="text/javascript" charset="utf-8">
  // Javascript magic that loads a users auth credentials into the Admin's
  // client and redirects to the user portal when ready.
</script>
{% endhighlight %}

However, traditional session-based auth use cases and myriad other custom
actions probably don't need a view like this and instead want more controller
logic. In this case you will want to override the controller logic by adding
something like this to the class in `impersonate_user.rb`:

{% highlight ruby %}
register_instance_option :controller do
  Proc.new do
    # Note: This is dummy code. The thing to note is that we aren't
    # rendering a view, just redirecting after taking an action on @object, which
    # will be the user instance in this case.
    @object.impersonate
    redirect_to back_or_index
  end
end
{% endhighlight %}

### Step 4: Customize Verbiage

Rails Admin will look in your `locales` to find tooltip and other verbiage that
will accompany your action:

{% highlight yaml %}
# config/locales/en.yml

en:
  admin:
    actions:
      impersonate_user:
        menu: 'Impersonate'
        title: 'Impersonating user...'
        breadcrumb: 'Impersonation'
{% endhighlight %}

This should get you up and running with a custom action in a way that is easy
to extend and maintain. Good luck!

[base-class]:  https://github.com/sferik/rails_admin/blob/master/lib/rails_admin/config/actions/base.rb
[rails-admin]: https://github.com/sferik/rails_admin
[case-study]: http://blog.endpoint.com/2012/03/railsadmin-custom-action-case-study.html
