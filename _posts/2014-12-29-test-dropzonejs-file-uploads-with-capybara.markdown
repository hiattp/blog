---
layout: post
title:  "Test Dropzone.js File Uploads With Capybara"
date:   2014-12-29 12:13:26
categories: rails testing capybara dropzonejs
meta: "Some tips and tricks to test file drag and drop uploads with Capybara."
---

Integration tests involving complex JS interactions are a pain, especially with
something like drag and drop file uploads (you can't exactly drag something into
a headless browser). My recent use case was an AngularJS application using [Dropzone.js][dropzone]
with Ruby on Rails on the backend, so I needed a way to make Dropzone play nicely
with Capybara Webkit. Here is the spec helper I ended up with:

{% highlight ruby %}
def drop_in_dropzone(file_path)
  # Generate a fake input selector
  page.execute_script <<-JS
    fakeFileInput = window.$('<input/>').attr(
      {id: 'fakeFileInput', type:'file'}
    ).appendTo('body');
  JS
  # Attach the file to the fake input selector with Capybara
  attach_file("fakeFileInput", file_path)
  # Add the file to a fileList array
  page.execute_script("var fileList = [fakeFileInput.get(0).files[0]]")
  # Trigger the fake drop event
  page.execute_script <<-JS
    var e = jQuery.Event('drop', { dataTransfer : { files : fileList } });
    $('.dropzone')[0].dropzone.listeners[0].events.drop(e);
  JS
end
{% endhighlight %}

Basically we need to get a file somewhere we can access it to simulate a drag,
so we create a fake file input and attach a file using the Capybara `attach_file`
helper. Then we simulate a drop event using jQuery to generate an event and the
`drop` handler in the Dropzone object attached to the element.

The first thing to note is that I had jQuery available, so it might be a bit
more complicated (but still possible) with vanilla JS. Another important
gotcha is that we can't use jQuery's [trigger][trigger] function like you
might expect, because the Dropzone events are not attached with `.on()`.

Using the helper might look something like this:

{% highlight ruby %}
feature 'My dropzone upload' do
  scenario 'a dropped file is uploaded' do
    visit '/upload_form'
    drop_in_dropzone Rails.root.join('spec/support/test.png')
    click_button 'Submit'
    expect(page.find('#uploaded-image')['src']).to match('test.png')
  end
end
{% endhighlight %}

[dropzone]: http://www.dropzonejs.com
[trigger]: http://api.jquery.com/trigger/
