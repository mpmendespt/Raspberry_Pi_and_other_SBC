---
layout: post
title: Dynamic DNS on Raspberry Pi
category: DNS DynDNS Raspberry Pi
---

How are web requests processed?
-------------------------------

When a user visits a web site, they use the site's domain name to
address the site. Their browser then sends a request to a DNS server to
translate the domain name into an IP address. Once the browser has the
site's IP address, it sends a request to the server.

There are two problems with this:

-   1\. the external IP address of your home network can change at any time,
    and 
-   2\. your Pi is behind a firewall and can't be accessed directly from
    the internet. 

Dynamic DNS
-----------

The first problem can be solved by using a [dynamic
DNS](http://en.wikipedia.org/wiki/Dynamic_DNS) service. These services
act as DNS servers that update automactically if your IP address
changes. There are numerous dynamic DNS services available. Most of them
provide a free service where you can choose a subdomain name.

You need to install a small piece of software on your Pi. This software
is supplied by your dynamic DNS provider, and it monitors the external
address of your router. If that address changes, the software sends a
message to the dynamic DNS server to update its records.

Port forwarding
---------------

When a user on the internet wants to see your web site, their browser
can get the IP address of your home network from your dynamic DNS
service. But requests still need to find a way through your router's
firewall.

By default web servers listen for connections on port 80. When a user's
request to see a page on your site reaches your router, the router must
forward that request to your Pi's IP address. You don't want to forward
all incoming traffic to your Pi, just the traffic for the web server
which is on port 80. Most routers allow you to set up port forwarding so
that any traffic on port 80 will be sent to your Pi.

### To create a domain name that always points to your home ip:

Goto [**www.noip.com**](http://www.noip.com/)[
](http://www.noip.com/)&gt; **create an account**

1.  Sign in to your noip account &gt; goto **Add Host**&gt; **create
    your host name with one of the offered domain
    names** (mpmendespt.ddns.net)
2.  Keep the **Host type** as **DNS Host A** ( If your ISP blocks Port
    80 for example, and you’re trying to run a webserver or other
    service on port 80, then you can choose Port 80 Redirect (at that
    point you’ll be asked to specify the port to use for
    the redirection)
3.  In the field marked **IP Address**: you should already see your
    current IP address.
4.  The next two options aren’t used for a basic account setup so leave
    them as they are.
5.  click the “**Add Host**” button at the bottom of the page to
    save it.

### Install No-IP’s Dynamic Update Client 

Create a directory for the client software:

****mkdir /home/pi/noip****

Download the client software:

****wget https://www.noip.com/client/linux/noip-duc-linux.tar.gz****

Extract the archive:

****tar zxvf noip-duc-linux.tar.gz****

Compile and install:

****sudo make****

****sudo make install****

After typing “sudo make install” you will be prompted to login with your
No-IP account username and password.

After logging into the DUC answer the questions to proceed. When asked
how often you want the update to happen you **must** choose 5 or more.
The interval is listed in minutes, if you choose 5 the update interval
will be 5 minutes. If you choose 30 the interval will be 30 minutes.

Please enter an update interval:\[30\] 10

Do you wish to run something at successful update?\[N\] (y/N) \^M

New configuration file '/tmp/no-ip2.conf' created.

mv /tmp/no-ip2.conf /usr/local/etc/no-ip2.conf

The Dynamic Update client is started by running:

**sudo /usr/local/bin/noip2**

To confirm that the service is working properly you can run the
following command:

**sudo noip2 -S**

### References 

* <http://raspberrywebserver.com/serveradmin/get-your-raspberry-pi-web-site-on-line.html>
* <http://www.techjawab.com/2013/06/setup-dynamic-dns-dyndns-for-free-on.html>
* <http://projpi.com/raspberry-pi-tips-and-hacks/raspberry-pi-2-on-dynamic-ip-and-noip/>
