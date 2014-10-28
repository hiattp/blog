---
layout: post
title:  "Image Processing With Thumbor Behind NGINX on EC2"
date:   2014-10-26 12:13:26
categories: ec2 thumbor
---
I'm a big fan of [thumbor](http://thumbor.org/) and resizing images on the fly
behind a CDN; what a great way to keep the front end flexible while seeing the
same\* performance as storing pre-sized images. When I'm working with a
fast-moving startup we don't want image processing API integrations; we want to
add a few settings in the img tag `src` url and see results. Strangely I only found a
couple services that do this, with [imgix][imgix] being the most prominent. I
may be searching the wrong thing, so I'd love see more options in the comments.
But meanwhile I didn't want to saddle my client with an extra $50 per month just
to see a bump in image performance, and their IP/image ownership was a concern.

### Enter Thumbor

There's a great [post by Yipit][yipit] on using a Thumbor-based solution at
scale, and apparently I completely missed out on a [more in-depth tutorial][tut]
when I set about borrowing Yipit's image strategy (you might head there if you want to
install on an Amazon Linux AMI, though I haven't tried Reed's steps myself).
I had an Ubuntu image ready to go so I thought
I'd write a short post on getting a quick-and-dirty\*\* image processor up and
running with a few `apt-get` commands. Go ahead and launch an Ubuntu EC2 image with
ports 22 and 80 exposed, `ssh` into it and follow along:

{% highlight bash shell %}
# Install nginx
sudo su
apt-get update
apt-get install nginx
/etc/init.d/nginx start
# Install Thumbor
apt-get install python-dev
apt-get install python-pip
apt-add-repository ppa:jon-severinsson/ffmpeg
apt-get update
apt-get install ffmpeg libjpeg-dev libpng-dev libtiff-dev libjasper-dev libgtk2.0-dev python-numpy python-pycurl webp python-opencv
ln -s /usr/lib/x86_64-linux-gnu/libjpeg.so /usr/lib
pip install pillow
pip install thumbor
thumbor-config > /etc/thumbor.conf
# Install Supervisor
easy_install supervisor
mkdir logs # For Supervisor logs
{% endhighlight %}

Now we just have a few config files to write. Again this is going to be
simplified---you'll probably want to do a deeper dive into the settings,
but this will get you started.

#### Supervisor Config File

{% highlight bash shell %}
# /etc/supervisord.conf

[supervisord]
[program:thumbor]
command=thumbor --port=800%(process_num)s
process_name=thumbor800%(process_num)s
numprocs=4
autostart=true
autorestart=true
startretries=3
stopsignal=TERM
stdout_logfile=/home/ubuntu/logs/thumbor800%(process_num)s.stdout.log
stdout_logfile_maxbytes=1MB
stdout_logfile_backups=10
stderr_logfile=/home/ubuntu/logs/thumbor800%(process_num)s.stderr.log
stderr_logfile_maxbytes=1MB
stderr_logfile_backups=10
{% endhighlight %}

#### Nginx Config File

{% highlight bash shell %}
# /etc/nginx/nginx.conf
# Put this under the http section, replacing the server name with
# your EC2 Public DNS

upstream thumbor {
    server 127.0.0.1:8000;
    server 127.0.0.1:8001;
    server 127.0.0.1:8002;
    server 127.0.0.1:8003;
}
server {
    listen 80;
    server_name ec2-53-236-234-31.compute-1.amazonaws.com;
    location / {
        proxy_pass http://thumbor;
    }
}
{% endhighlight %}

A few more commands will wrap up this shindig:

{% highlight bash shell %}
# Start Supervisor
supervisord -c /etc/supervisord.conf
# Restart nginx
service nginx restart
{% endhighlight %}

Voilà, image processing server ready to go. Try the thumbor example image by navigating
here in your browser:

    http://<your-public-dns>/unsafe/300x200/http://www.waterfalls.hamilton.ca/images/Waterfall_Collage_home_sm1.jpg

There are a few more things you'll want to do before you use this in a
production environment (probably more than a few). To name some:

1. Assign your instance an Elastic IP
2. Put the instance behind a CDN like CloudFront
3. Read about and implement [Thumbor Security Measures][security]
4. Configure your [image storage][storage] depending on your needs/resources
5. Other Thumbor config, app monitoring, and all the other fun stuff that comes
   along with your new "custom" image processing solution

That being said, it is pretty exciting to introduce even a simple version of
this stack in your product. If you are iterating on thumbnail sizes while your
early adopters are uploading large images even the simple implementation above
will give you huge performance gains, and you can focus on optimizing
security/storage/etc as your business matures.

##### \* Close enough given the benefits :)

##### \*\* I'm going to ignore/omit a few things like [thumbor security][security]. Head to Reed's the more [in-depth post][tut] for something more comprehensive.

[yipit]: http://tech.yipit.com/2013/01/03/how-yipit-scales-thumbnailing-with-thumbor-and-cloudfront/
[imgix]: http://www.imgix.com/
[tut]:   http://www.dadoune.com/blog/best-thumbnailing-solution-set-up-thumbor-on-aws/
[security]: https://github.com/thumbor/thumbor/wiki/Security
[storage]:  https://github.com/thumbor/thumbor/wiki/Image-storage
