---
layout: post
title:  "Filter Wireshark Packets by Protocol"
date:   2015-07-26 12:13:26
categories: wireshark
meta: "Why was this so difficult to figure out?"
---

If you've ever tried to monitor telnet or HTTP traffic to a specific IP
address with Wireshark (or more likely the loopback for localhost) you'll have
been frustrated by the various packets that have nothing to do with what you
want. Wireshark issues seem particularly difficult to troubleshoot via Google so
more as a reminder to myself, this is a filter that will only display telnet
communications from a specific IP:

    (telnet) && ip.src==172.14.13.123
