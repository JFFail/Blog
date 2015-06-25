---
layout: post
title: "Configure Nginx To Force SSL"
date: 2015-06-25 14:12:00
categories: nginx server ssl https
---
When I set up this blog one of the things I had to consider was how I wanted to serve it up. I could have easily used the `jekyll serve` command to have Jekyll host itself. I didn't really like that idea, though; I wanted to have a dedicated web server back-end running the static HTML pages that Jekyll parsed together for me. I opted to go with [Nginx][nginx] over Apache just because it seems to be the new hotness; I figured that keeping myself up to speed on the latest and greatest (even if it's the latest and greatest in an area where I don't normally work, as is the case here) would be good for me.

Getting Nginx up and running was easy enough; there are plenty of good tutorials online. My next step was to leverage an SSL certificate so that I could deliver content over HTTPS. This was slightly less clear to me. I basically went underneath my existing config under **/etc/nginx/sites-available** and just started adding stuff to it inside of my existing **server** setup. It worked, but unbeknownst to me was far from ideal. I realized my mistake later on, as we'll see in a moment.

My next step was to set up a redirect because I didn't actually *want* anyone using HTTP with the site. If HTTPS is available, why allow for HTTP? I would imagine that HTTP traffic would become common from people not specifying the protocol when typing the URL into the address bar or for hyperlinks. When researching this, I realized that I should have my port 80 setup and my port 443 setup under *separate* **server** definitions within the same configuration file under **sites-available**. It looks like this:

    server {
        listen 80 default_server;
        listen [::]80 default_server;
        server_name url.here;
        return 301 https://$server_name$request_uri;
    }
    
    server {
        listen 443 ssl default_server;
        listen [::]:443 ssl default_server;
    
        ssl on;
        ssl_certificate /path/to/public/cert;
        ssl_certificate_key /path/to/private/key;

        root /path/to/site;

        index index.html index.htm;

        server_name url.here;
    }    

So as you can see here, I actually have two different **server** definitions. The first handles port 80 traffic while the second handles port 443 traffic, both operating for the same site. The key I was able to [find eventually][force-https] is the `return 301 https://$server_name$request_uri;` line. This tells Nginx that any time it receives a request on port 80 to redirect that request to 443. After this, I just had to restart the service:

    sudo service nginx restart

Finally I was able to confirm that even when nagivating directly to [http://mads.ninja][mads] I would get redirected to the HTTPS version like I'd expect. Awesome!

[nginx]:    http://nginx.org/
[force-https]: http://serverfault.com/questions/67316/in-nginx-how-can-i-rewrite-all-http-requests-to-https-while-maintaining-sub-dom
[mads]: http://mads.ninja
