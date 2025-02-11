+++
title = "Configure nginx to server multiple domains / subdomains"
slug = "2014-03-05-configure-nginx-to-server-multiple-domains-subdomains"
published = 2014-03-05T03:06:00.001000-08:00
author = "Pandurang Patil"
tags = ["nginx"]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">With
nginx it is quite easy to configure multiple domains or subdomains to be
served from single server. Refer following configuration for the
same.</span>  

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>

        server {
            server_name first.pandurangpatil.com;
            root /var/www/first;
        }

        server {
            server_name second.pandurangpatil.com;
            root /var/www/second;
        }

        server {
            server_name someother.com;
            root /var/www/other;
        }

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>
