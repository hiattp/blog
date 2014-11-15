---
layout: post
title:  "Paperclip and S3 Gotcha: PermanentRedirect - The bucket must be addressed using the specified endpoint"
date:   2014-11-15 12:13:26
categories: rails paperclip s3
meta: "The bucket you are attempting to access must be addressed using the specified endpoint. Please send all future requests to this endpoint."
---
I've been using Paperclip for uploading files to S3 in Rails apps for years without
issue, so I was a bit peeved when I hit this error today in a standard
implementation:

{% highlight xml %}
<Error>
  <Code>PermanentRedirect</Code>
  <Message>
    The bucket you are attempting to access must be addressed using the specified endpoint. Please send all future requests to this endpoint.
  </Message>
  <Bucket>myapp-development</Bucket>
  <Endpoint>myapp-development.s3.amazonaws.com</Endpoint>
  <RequestId>7730ELL6LL4LL37AD7</RequestId>
  <HostId>
    PJmWsvssoMEuA9yo6fkjkja2323sssfa
  </HostId>
</Error>
{% endhighlight %}

A bit of Googling revealed that this only happens on S3 buckets provisioned
outside of the US (I was dropping one in the Singapore zone). Apparently the
default for Paperclip is to use the "path style" for image URLs:

    s3.amazonaws.com/bucket

Instead of the "domain" style:

    bucket.s3.amazonaws.com

According to the [docs][docs] the domain style works when the path style does
not, which begs the question: Why is path style the default?

> Normally, this won't matter in the slightest and you can leave the default
(which is path-style, or :s3_path_url). But in some cases paths don't work and
you need to use the domain-style (:s3_domain_url). Anything else here will be
treated like path-style.

So we need to set the `:url` option in our `has_attached_file` config to
`:s3_domain_url`. But here is another gotcha---that attribute needs to be a
string version of the symbol, so your config will have to look like this:

{% highlight ruby %}
has_attached_file :avatar,
    :styles => { :medium => "300x300>", :thumb => "100x100>" },
    :url => ":s3_domain_url",
    :path => 'users/:id/avatar/:style_:basename.:extension',
    :storage => :s3,
    :bucket => ENV['S3_BUCKET'],
    :s3_credentials => {
      :access_key_id => ENV['S3_KEY'],
      :secret_access_key => ENV['S3_SECRET']
    }
{% endhighlight %}

[docs]: http://www.rubydoc.info/gems/paperclip/Paperclip/Storage/S3
